##  交换机与控制器交互
我们可以启动一个简单的控制器，默认没有任何流表项，仅仅作为一台带学习功能的交换机。控制器默认监听端口是 6633。

以下控制器与交换机之间的消息交互过程，可以通过 wireshark，配置 of 过滤器观察到交换机跟控制器之间的交互消息。
参见下面的表格。

| 消息 | 类型 | 描述 |
| -- | -- | -- |
| Hello | Controller->Switch | 跟着 TCP 握手，控制器发送它的版本号到交换机。|
| Hello | Switch->Controller | 交换机回复它支持的版本。|
| Features Request | Controller->Switch | 控制器询问可用端口。|
| Set Config | Controller->Switch | 控制器让交换机发送流超时消息。|
| Features Reply | Switch->Controller | 交换机回复端口、端口速度、支持的表和行动。|


同样，我们可以用 wireshark 观察到当第一次有 ping 包从 h2 发到 h3 时，控制器如何自动添加相应的表项到交换机。wireshark 相应的过滤器为 `of && (of.type != 3) && (of.type != 2)`。

相关的消息过程参考下面的表格。
| 消息 | 类型 | 描述 |
| -- | -- | -- |
| Packet-In | Switch->Controller | 网包到达交换机，没有发生匹配，发送到控制器。|
| Packet-Out | Controller->Switch | 从交换机端口发出包。|
| Flow-Mod | Controller->Switch | 添加指定流。|
| Flow-Expired | Switch->Controller | 流超时。|

