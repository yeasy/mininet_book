## 使用 dpctl
执行
```
dpctl show tcp:127.0.0.1:6634
```
可以查看到交换机的端口等基本情况，其中 tcp 端口 6634 是默认的交换机监听端口。

执行
```
dpctl dump-flows tcp:127.0.0.1:6634
```
可以看到更详细的流表信息。
此时，流表为空，执行 `h2 ping h3` 无法得到响应。因此我们需要通过 dpctl 手动添加流表项，实现转发。
命令为
```
dpctl add-flow tcp:127.0.0.1:6634 in_port=1,actions=output:2
dpctl add-flow tcp:127.0.0.1:6634 in_port=2,actions=output:1
```
此时查看流表可以看到新的转发信息，同时可以在 h2 和 h3 之间 ping 通。

