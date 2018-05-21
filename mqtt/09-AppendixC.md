# 附录C MQTT v5.0新特性总结（非规范）

## 目录

- [第一章 - 介绍](01-Introduction.md)
- [第二章 – MQTT控制报文格式](02-ControlPacketFormat.md)
- [第三章 – MQTT控制报文](03-ControlPackets.md)
- [第四章 – 操作行为](04-OperationalBehavior.md)
- [第五章 – 安全（非规范）](05-Security.md)
- [第六章 – 使用WebSocket](06-WebSocket.md)
- [第七章 – 一致性目标](07-Conformance.md)
- [附录B - 强制性规范声明（非规范）](08-AppendixB.md)
- [附录C - MQTT v5.0新特性总结（非规范）](09-AppendixC.md)

MQTT v5.0添加了以下特性  

•	会话过期
把清理会话标志拆分成新开始标志（指示会话应该在不使用现有会话的情况下开始）和会话过期间隔标志（指示连接断开之后会话保留的时间）。会话过期间隔时间可以在断开时修改。把新开始标志设置为1且会话过期间隔标志设置为0，等同于在MQTT v3.1.1中把清理会话（CleanSession）设置为1。

•	消息过期
允许消息在发布时设置一个过期间隔。

•	所有确认报文原因码
更改所有响应报文以包含原因码，包括CONNACK，PUBACK，PUBREC，PUBREL，PUBCOMP，SUBACK，UNSUBACK，DISCONNECT和AUTH，以使得调用方确定请求的函数是否成功。

•	所有确认报文原因字符串
更改大部分报文以包含原因码同时也允许一个可选的原因字符串。这是为问题定位而设计的，并且不应由接收端所解析。

•	服务端断开
允许服务端发送DISCONNECT报文，以指示连接被关闭的原因。 

•	载荷格式和内容类型
允许在消息发布时指定载荷格式（二进制、文本）和MIME样式内容类型。这些信息被转发到消息的接收端。

•	请求/响应
规定MQTT请求/响应模式，提供响应主题和对比数据属性，以使得响应消息被路由回请求的发布者。此外，为客户端添加从服务端获取获取关于构造响应主题的配置信息的能力。

•	共享订阅
添加对共享订阅的支持，以允许多个订阅消费者进行负载均衡。

•	订阅标识符
允许在SUBSCRIBE报文中指定一个数字订阅标识符，并在消息分发时返回此标识符。这使得客户端收到分发的消息时确定此消息是由哪个或哪些订阅导致的。

•	主题别名
通过将主题名缩写为小整数来减小MQTT报文的开销大小。客户端和服务端分别指定它们允许的主题别名的数量。

•	流量控制
允许客户端和服务端分别指定未完成的可靠消息（QoS>0）的数量。发送端可以暂停发送此类消息以保持消息数量低于配额。这被用于限制可靠消息的速率和某一时刻的传输中（in-flight）消息数量。

•	用户属性
为大多数报文添加用户属性。PUBLISH报文的用户属性由客户端应用程序定义。PUBLISH报文和遗嘱报文的用户属性由服务端转发给应用消息的接收端。CONNECT，SUBSCRIBE和UNSUBSCRIBE报文的用户属性由服务端实现定义。CONNACK，PUBACK，PUBREC，PUBREL，PUBCOMP，SUBACK，UNSUBACK和AUTH报文的用户属性由发送端定义，且对发送端具有唯一性。MQTT规范不定义用户属性的意义。

•	最大报文长度
允许客户端和服务端各自指定它们支持的最大报文长度。会话参与方发送更大的报文将造成错误。

•	可选的服务端功能可用性
提供定义一组服务端不允许的功能，并告知客户端的机制。可以使用这种方式指定的功能包括：最大QoS等级，保留可用，通配符订阅可用，订阅标识符可用和共享订阅可用。客户端使用服务端通知了（不可用）的功能将造成错误。 

在早期版本的MQTT协议中，服务端没有实现的功能通过未授权告知客户端。当客户端使用其中一种（不可用的）功能时，此功能允许服务端告知客户端，并添加特定的原因码。

•	增强的认证
提供一种机制来启用包括互相认证在内的质询/响应风格的认证。这允许在客户端和服务端都支持的情况下使用SASL风格的认证，包括客户端在连接中重新认证的功能。

•	订阅选项
提供主要用于定义允许消息桥接应用的订阅选项。包括不要把消息发送给消息源客户端（非本地）的选项和订阅时处理保留消息的选项。

•	遗嘱延迟
提供指定遗嘱消息在连接中断后延时发送的能力。设计此特性是为了在会话的连接重建的情况下不发送遗嘱消息。此特性允许连接短暂中断而不通知其他客户端。

•	服务端保持连接
允许服务端指定其希望客户端使用的保持连接值。此特性允许服务端设置最大允许的保持连接值并被客户端使用。

•	分配客户标识符
服务端分配了客户标识符的情况下，向客户端返回此客户标识符。服务端分配客户标识符只能用于新开始标志为1的连接。

•	服务端参考
允许服务端使用CONNACK或DISCONNECT报文指定备用服务端。此特性被用于（服务端）重定向或做准备。


### 项目主页

- [MQTT协议中文版](https://github.com/hui6075/mqtt_v5)

