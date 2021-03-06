# http工作原理

HTTP协议（HyperText Transfer Protocol，超文本传输协议）是用于从WWW服务器传输超文本到本地浏览器的传送协议。它可以使浏览器更加高效，使网络传输减少。它不仅保证计算机正确快速地传输超文本文档，还确定传输文档中的哪一部分，以及哪部分内容首先显示(如文本先于图形)等。



### 计算机之间相互通信

 互联网的关键技术就是TCP/IP协议。两台计算机之间的通信是通过TCP/IP协议在因特网上进行的。实际上这个是两个协议：

​    TCP : Transmission Control Protocol 传输控制协议和IP： Internet Protocol 网际协议。

​    IP：计算机之间的通信

​     IP协议是计算机用来相互识别的通信的一种机制，每台计算机都有一个IP.用来在internet上标识这台计算机。 IP 负责在因特网上发送和接收数据包。通过 IP，消息（或者其他数据）被分割为小的独立的包，并通过因特网在计算机之间传送。IP 负责将每个包路由至它的目的地。

​    IP协议仅仅是允许计算机相互发消息，但它并不检查消息是否以发送的次序到达而且没有损坏（只检查关键的头数据）。为了提供消息检验功能，直接在IP协议上设计了传输控制协议TCP.

​    

​    TCP : 应用程序之间的通信

​    TCP确保数据包以正确的次序到达，并且尝试确认数据包的内容没有改变。TCP在IP地址之上引端口（port），它允许计算机通过网络提供各种服务。一些端口号为不同的服务保留，而且这些端口号是众所周知。

​    服务或者守护进程：在提供服务的机器上，有程序监听特定端口上的通信流。例如大多数电子邮件通信流出现在端口25上，用于wwww的HTTP通信流出现在80端口上。

​    当应用程序希望通过 TCP 与另一个应用程序通信时，它会发送一个通信请求。这个请求必须被送到一个确切的地址。在双方“握手”之后，TCP 将在两个应用程序之间建立一个全双工 (full-duplex) 的通信，占用两个计算机之间整个的通信线路。TCP 用于从应用程序到网络的数据传输控制。TCP 负责在数据传送之前将它们分割为 IP 包，然后在它们到达的时候将它们重组。

​    TCP/IP 就是TCP 和 IP 两个协议在一起协同工作，有上下层次的关系。

​    TCP 负责应用软件（比如你的浏览器）和网络软件之间的通信。IP 负责计算机之间的通信。TCP 负责将数据分割并装入 IP 包，IP 负责将包发送至接收者，传输过程要经IP路由器负责根据通信量、网络中的错误或者其他参数来进行正确地寻址，然后在它们到达的时候重新组合它们。



### HTTP工作过程 

 一次HTTP操作称为一个事务，其工作整个过程如下：

   1 ) 、地址解析，

   如用客户端浏览器请求这个页面：[http://localhost.com:8080/index.htm](http://localhost:8080/simple.htm)

   从中分解出协议名、主机名、端口、对象路径等部分，对于我们的这个地址，解析得到的结果如下：
   协议名：http
   主机名：localhost.com
   端口：8080
   对象路径：/index.htm

   在这一步，需要域名系统DNS解析域名localhost.com,得主机的IP地址。


  2）、封装HTTP请求数据包

   把以上部分结合本机自己的信息，封装成一个HTTP请求数据包


   3）封装成TCP包，建立TCP连接（TCP的三次握手）

​    在HTTP工作开始之前，客户机（Web浏览器）首先要通过网络与服务器建立连接，该连接是通过TCP来完成的，该协议与IP协议共同构建Internet，即著名的TCP/IP协议族，因此Internet又被称作是TCP/IP网络。HTTP是比TCP更高层次的应用层协议，根据规则，只有低层协议建立之后才能进行更高层协议的连接，因此，首先要建立TCP连接，一般TCP连接的端口号是80。这里是8080端口

   4）客户机发送请求命令

​    建立连接后，客户机发送一个请求给服务器，请求方式的格式为：统一资源标识符（URI：Uniform Resource Identifier）、协议版本号，后边是MIME信息包括请求修饰符、客户机信息和可能的内容。

   5）服务器响应

   服务器接到请求后，给予相应的响应信息，其格式为一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容。

​    实体消息是服务器向浏览器发送头信息后，它会发送一个空白行来表示头信息的发送到此结束，接着，它就以Content-Type应答头信息所描述的格式发送用户所请求的实际数据

   6）服务器关闭TCP连接

   一般情况下，一旦Web服务器向浏览器发送了请求数据，它就要关闭TCP连接，然后如果浏览器或者服务器在其头信息加入了这行代码

  Connection:keep-alive

  TCP连接在发送后将仍然保持打开状态，于是，浏览器可以继续通过相同的连接发送请求。保持连接节省了为每个请求建立新连接所需的时间，还节约了网络带宽。



















### HTTPS实现原理  

 

​       HTTPS（全称：Hypertext Transfer Protocol over Secure Socket Layer），是以安全为目标的HTTP通道，简单讲是HTTP的安全版。即HTTP下加入SSL层，HTTPS的安全基础是SSL。其所用的端口号是443。

 

​     SSL：安全套接层，是netscape公司设计的主要用于web的安全传输协议。这种协议在WEB上获得了广泛的应用。通过证书认证来确保客户端和网站服务器之间的通信数据是加密安全的。

 

 

   有两种基本的加解密[算法](http://lib.csdn.net/base/datastructure)类型：

   1）对称加密（symmetric encryption）：密钥只有一个，加密解密为同一个密码，且加解密速度快，典型的对称加密[算法](http://lib.csdn.net/base/datastructure)有DES、AES，RC5，3DES等；

​    对称加密主要问题是共享秘钥，除你的计算机（客户端）知道另外一台计算机（服务器）的私钥秘钥，否则无法对通信流进行加密解密。解决这个问题的方案非对称秘钥。

   2）非对称加密：使用两个秘钥：公共秘钥和私有秘钥。私有秘钥由一方密码保存（一般是服务器保存），另一方任何人都可以获得公共秘钥。

   这种密钥成对出现（且根据公钥无法推知私钥，根据私钥也无法推知公钥），加密解密使用不同密钥（公钥加密需要私钥解密），相对对称加密速度较慢，典型的非对称加密算法有RSA、DSA等。

  下面看一下https的通信过程：

​    1） SSL客户端通过TCP和服务器建立连接之后（443端口），并且在一般的tcp连接协商（握手）过程中请求证书。

​       即客户端发出一个消息给服务器，这个消息里面包含了自己可实现的算法列表和其它一些需要的消息，SSL的服务器端会回应一个数据包，这里面确定了这次通信所需要的算法，然后服务器向客户端返回证书。（证书里面包含了服务器信息：域名。申请证书的公司，公共秘钥）。         

​    2）Client在收到服务器返回的证书后，判断签发这个证书的公共签发机构，并使用这个机构的公共秘钥确认签名是否有效，客户端还会确保证书中列出的域名就是它正在连接的域名。

​    3）  如果确认证书有效，那么生成对称秘钥并使用服务器的公共秘钥进行加密。然后发送给服务器，服务器使用它的私钥对它进行解密，这样两台计算机可以开始进行对称加密进行通信。

 

https通信的优点：

1）客户端产生的密钥只有客户端和服务器端能得到；

2）加密的数据只有客户端和服务器端才能得到明文；

3）客户端到服务端的通信是安全的。







 

 

