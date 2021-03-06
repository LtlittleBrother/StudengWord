# TCP/IP协议族

## 分层 

![](F:\AndroidProject\StudentWord\app\src\main\assets\tcpip简单模型.png)

>+ 为什么要分层？

>>+ 因为显示网络的不稳定性

>>+ 具体分层:

>>>+ Application Layer 应用程：HTTP、FTP、DNS

>>>+ Transport layer 传输层（负责拼装数据等，拼装完了给网络层去发送）: TCP(具有稳定性，对方主机收到后会有一个回执，如果一定时间内没有收到回执则从新发一次)、UDP(不具有稳定性，不会重发数据。比如直播、游戏等场景)

>>>+ Internet Layer 网络层（只管发送数据，传输层给一段数据发送以此数据，不管数据拼接组装）: IP

>>>+ Link Layer 数据链路层: 以太网、wifi路由等

## TCP连接

>+ 什么叫连接？

>>+ TCP是一种有状态(我给你发消息的时候你已经认识我了，不需要每次发消息的时候都给目标主机自我介绍了，这就是有状态)的交互,利用端口(收发器)让两端互相认识的过程叫做连接。

>>+ TCP连接的建立:

>>>+ 可以这么理解： 

>>>>+ 客户端给服务端说："我要给你发消息了"

>>>>+ 服务端收到消息后回复:"我知道了,我也要给你发消息了"

>>>>+ 客户端收到回复后:"我知道了"。就建立了连接

![](F:\AndroidProject\StudentWord\app\src\main\assets\TCP连接的建立.png)

>>+ TCP连接的关闭:

>>>+ 可以这么理解： 

>>>>+ 客户端给服务端说:"我没有消息要给你发了" 

>>>>+ 服务端回复客户端:"我知道了"

>>>>+ 服务端回复客户端："我也没有消息要给你发了";服务端分两次做回应是因为客户端没有消息发了，但服务端这边可能还有消息要发送；所以当服务端也没有消息发了后在回复客户端

>>>>+ 客户端回复服务端："我知道了"。就关闭了连接

>>>+ 为什么要关闭？因为一直连接会浪费资源，当没有数据要发送时应及时关闭连接


![](F:\AndroidProject\StudentWord\app\src\main\assets\TCP连接的关闭.png)


>+ TCP长连接

>>+ 为什么要长连接?

>>>+ 因为目前大多数网络都是内网环境，通过别的基站转发出去连接的外网，如果长时间双方不发送消息，基站就会给你把端口关闭了，这样的话客户端方就被动关闭了连接，所以需要长连接

>>+ 长连接的实现方式

>>>+ 心跳：就是指每隔一段时间发送以此很小的数据给对方，以此来保证端口不会被基站误关闭，来实现长连接。

