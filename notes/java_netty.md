############################

############################
# JAVA NETTY
############################

############################

# Netty
tcp veya udp'den haberleşmeleri için kullanılan java kütüphanesi.

netty ile udp soketlerine de bağlanılabilir, http istekleri deyapılıp alınabilir. birçok bağlantı çeşidi resmi olarak destekleniyor fakat farklı bağlantı çeşitleri de implemente edilebilir.

netty ile bağlantı kurulan tarafın netty kullanmasını gerektirmez.

örnek basit bir client kodu:

```java
// grup'lar ile istediğimiz kadar bağlantıyı kolayca yönetebiliyoruz. (bu durum finally kısmında güzel olarak örneklendirilecek)
EventLoopGroup group = new NioEventLoopGroup();

try{
    // Bootstrap genel nesne. bunsuz da olur fakat iş çok uzar.
    Bootstrap clientBootstrap = new Bootstrap();
    
    // her Bootstrap'in hangi gruba dahil olduğunu belirliyoruz. istersek birden fazla gruba da dahil yapabiliriz.
    clientBootstrap.group(group);

    // channel = bağlantı. NioSocketChannel bir çeşit soket çeşidi. birçok çeşit var. NioSocketChannel en temel tcp objesi.
    clientBootstrap.channel(NioSocketChannel.class);

    // gerçek soket nesnemizi Bootstrap'e bind ediyoruz. bunu yapmasaydık aşağıdaki bulunan connect metoduna parametre olarak ip portu yollamalıydık, connect bizim yerimize gerçek soket nesnesi oluşturacaktı.
    clientBootstrap.remoteAddress(new InetSocketAddress("localhost", 9999));

    // her channel'a birden fazla handler atayabiliriz. handler atama işlemlerini ChannelInitializer ile yapmalıyız.
    clientBootstrap.handler(new ChannelInitializer<SocketChannel>() {
        
        protected void initChannel(SocketChannel socketChannel) throws Exception {

            // birden fazla handler ekleyebiliriz. bir data gönderildiğinde yada alındığında handlerlar sırası ile çalıştırılır. addLast, addFirst ile handler'ların sıralarını belirlemekteyiz.
            // handlerlar tıpkı servletlerdeki filter'lar gibi düşünülebilir. data (request), sırası ile her filter'a uğraması gibi...
            socketChannel.pipeline().addLast(new ClientHandler());
        }
    });

    // clientBootstrap connect metodu ip'ye bağlantı yapıyor ve return olarak ChannelFuture döndürüyor.
    // ChannelFuture, java.util.concurrent.Future'den türemiştir. java'nın Future'ının özelleştirilmiş halidir.
    // ChannelFuture metodunun sync metodu, Future'ın bitmesini bekliyor. async durumlarda bunu kullanmamak gerekli. burada örnek olsun diye kullandık.
    ChannelFuture channelFuture = clientBootstrap.connect().sync();

    // channel() metodu channel'ı döndürüyor.
    // closeFuture(); ChannelFuture döndürüyor, ama bu ChannelFuture kapanma event'ini baz alarak çalışıyor. yani; yukarıdaki ChannelFuture soket bağlanınca Future objesinin taskı done oluyordu (tamamlanıyordu). aşağıdaki satırdaki channelFuture (closeFuture()'dan dönen obje) ancak soket kapandığında done oluyor.
    // sync metodu future'nin done olmasını bekliyor. sync tamamen önrke olduğu için bu satırda kullanıldı.
    channelFuture.channel().closeFuture().sync();
} finally {
    // group yapmamızın avantajı bu. bu gruba bağlı tüm Bootstrap'lere tek bir yerden aynı çağrıyı yapabiliyoruz.
    group.shutdownGracefully().sync();
}
```

Chaneller'lar 2 farklı gruba ayrılır:
- ChannelInboundHandler: soketimize istek geldiğinde bu channel'lardan sıra ile geçer
- ChannelOutboundHandler: soketimizden istek yolladığımızda bu channel'lardan sıra ile çıkar

client kodumuza devam edelim:

```java
//channel'larında bir çok implementasyonu/çeşidi var. bazıları generic yapıda olup, byte, string bazında okuma yazma yapabilmemizi sağlıyor.
public class ClientHandler extends SimpleChannelInboundHandler {

    @Override
    //bu metod soket aktif olduğunda (bağlantı açıldığı anda devreye giriyor)
    public void channelActive(ChannelHandlerContext channelHandlerContext){
        channelHandlerContext.writeAndFlush(Unpooled.copiedBuffer("Netty Rocks!", CharsetUtil.UTF_8));
    }

    @Override
    //channel'a istek geldiğinde çalışıyor
    public void channelRead0(ChannelHandlerContext channelHandlerContext, ByteBuf in) {
        System.out.println("Client received: " + in.toString(CharsetUtil.UTF_8));
    }

    @Override
    //herhangi bir yerde hata olduunda çalışıyor
    public void exceptionCaught(ChannelHandlerContext channelHandlerContext, Throwable cause){
        cause.printStackTrace();
        channelHandlerContext.close();
    }
}
```

server kodu da neredeyse tamamen benzer yapıda:

```java
EventLoopGroup group = new NioEventLoopGroup();

try{
    ServerBootstrap serverBootstrap = new ServerBootstrap();
    serverBootstrap.group(group);
    serverBootstrap.channel(NioServerSocketChannel.class);
    serverBootstrap.localAddress(new InetSocketAddress("localhost", 9999));

    serverBootstrap.childHandler(new ChannelInitializer<SocketChannel>() {
        protected void initChannel(SocketChannel socketChannel) throws Exception {
            socketChannel.pipeline().addLast(new HelloServerHandler());
        }
    });
    ChannelFuture channelFuture = serverBootstrap.bind().sync();
    channelFuture.channel().closeFuture().sync();
} catch(Exception e){
    e.printStackTrace();
} finally {
    group.shutdownGracefully().sync();
}
```

```java
public class HelloServerHandler extends ChannelInboundHandlerAdapter {

    @Override
    public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
        ByteBuf inBuffer = (ByteBuf) msg;

        String received = inBuffer.toString(CharsetUtil.UTF_8);
        System.out.println("Server received: " + received);

        ctx.write(Unpooled.copiedBuffer("Hello " + received, CharsetUtil.UTF_8));
    }

    @Override
    public void channelReadComplete(ChannelHandlerContext ctx) throws Exception {
        ctx.writeAndFlush(Unpooled.EMPTY_BUFFER)
                .addListener(ChannelFutureListener.CLOSE);
    }

    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) throws Exception {
        cause.printStackTrace();
        ctx.close();
    }
}
```

# Codec
netty dünyasında codec; channel implementasyonu anlamına gelir. gelen isteği parse eder ve bize java objelerine çevirir. biz gelen datayı hazır şekilde java objelerinden okuruz.

# ChannelPipeline
her channel'ın bir pipeline'ı vardır. bu obje handler'ların listesini sırası ile tutar.  hem outbound hemde inbound handler'lar bu objenin içerisindedir.
