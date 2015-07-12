##计算机网络基础知识

####OSI七层模型和TCP/IP五层模型


        应用层
        表示层                  应用层
        会话层
        传输层                  传输层
        网络层                  网际层
        数据链路层              
        物理层                  网络接口层
        
        
        数据链路层：负责分配MAC地址
        网络层：负责对数据包进行路由选择和存储转发。网络层协议有：IP、ICMP、IGMP、ARP、RARP、OSPF
        传输层：是第一个端到端，即进程到进程的层次。传输层协议：TCP、UDP
        应用层：为操作系统或者网络应用程序提供访问网络服务的接口。应用层协议：RIP、TELNET、FTP、HTTP、SNMP


####TCP三次握手

        SYN     同步序号，表示报文是一个连接请求或连接接受报文
        ACK     确认位，对接收到报文的确认

        1）客户端向服务器发送一个SYN J;
        
        2）服务器向客户端响应一个SYN K，并对 SYN J 进行确认 ACK J+1;
        
        3）客户端再向服务器发送一个确认 ACK K+1。


####TCP四次挥手

        FIN     终止位，表示发送方完成数据发送，用来释放一个连接
        
        1）某个应用程序首先调用close，我们称这一端执行主动关闭。这一端的TCP于是发送一个FIN分节，表示数据发送完毕；
        
        2）另一端接受FIN分节后，执行被动关闭，对这个FIN进行确认。它的接收也作为文件结束符传递给接收端应用进程，因为FIN
        的接收意味着应用进程在相应的连接上再也接收不到额外数据；
        
        3）一段时间之后，接收到文件结束符的应用进程调用close关闭它的套接口。这导致它的TCP也发送一个FIN;
        
        4）接收到这个FIN的原发送端TCP（即执行主动关闭的那一端）对它进行确认。


####TCP为何采用三次握手，两次行吗？

        两次不行，采用三次握手是为了防止失效的连接请求报文段突然又传送到服务器，从而发生错误。当客户端发出的连接请求报
        文段由于某些原因没有及时到达服务器，而客户端等待一段时间后，又重新向服务器发送连接请求，且建立成功，顺序完成数
        据传输，那么第一次发送的连接请求报文段就称为失效的连接请求报文段。
        考虑这样一种特殊情况，客户端第一次发送的连接请求并没有丢失，而是因为网络问题导致延迟到达服务器，服务器以为是客
        户端又发起的新连接，于是服务器同意连接，并向客户端发回确认，但是此时客户端不予理会，服务器就一直等待客户端发送
        数据，导致服务器资源浪费。



####在浏览器里输入URL地址回车后，发生了些什么？

        1）进行寻址：如果在浏览器的缓存中存有URL对应的IP，则直接查询其IP；否则，访问DNS（Domain Name System）进行寻址。
        
        2）DNS或者 URL cache 返回网页服务器的IP地址。
        
        3）浏览器与服务器通过三次握手建立TCP连接。由于是网页服务器，故浏览器连接到服务器的80端口。
        
        4）浏览器与服务器建立HTTP会话（session），接收来自服务器的HTTP数据。
        
        5）浏览器解析HTTP数据，在本地窗口内渲染并显示网页。
        
        6）当浏览器页面被关闭时，终止HTTP会话并关闭连接。
        
        
        