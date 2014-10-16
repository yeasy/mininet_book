##  常用命令总结
* `help` 默认列出所有命令文档，后面加命令名将介绍该命令用法
* `dump` 打印节点信息
* `gterm` 给定节点上开启 gnome-terminal。注：可能导致 Mininet 崩溃
* `xterm` 给定节点上开启 xterm
* `intfs` 列出所有的网络接口
* `iperf` 两个节点之间进行简单的 iperf TCP测试
* `iperfudp` 两个节点之间用指定带宽 udp 进行测试
* `net` 显示网络链接情况
* `noecho` 运行交互式窗口，关闭回应（echoing）
* `pingpair` 在前两个主机之间互 ping 测试
* `source` 从外部文件中读入命令
* `dpctl` 在所有交换机上用 dptcl 执行相关命令，本地为 `tcp 127.0.0.1:6634`
* `link` 禁用或启用两个节点之间的链路
* `nodes` 列出所有的节点信息
* `pingall` 所有 host 节点之间互 ping
* `py` 执行 Python 表达式
* `sh` 运行外部 shell 命令
* `quit/exit` 退出
