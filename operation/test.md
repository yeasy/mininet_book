## 快捷测试
除了 cli 的交互方式之外，Mininet 还提供了更方便的自动执行的快捷测试方式，其格式为 `sudo mn --test cmd`，即可自动启动并执行 cmd 操作，完成后自动退出。

例如 `sudo mn --test pingpair`，可以直接对主机连通性进行测试，`sudo mn --test iperf`启动后直接进行性能测试。用这种方式很方便直接得到实验结果。
