## 启动参数总结

* `-h, --help` 打印帮助信息
* `--switch=SWITCH` 交换机类型，包括 [kernel user ovsk]
* `--host=HOST` 模拟主机类型，包括 [process]
* `--controller=CONTROLLER` 控制器类型，包括 [nox_dump none ref remote nox_pysw]
* `--topo=TOPO,arg1,arg2,...argN` 指定自带拓扑，包括 [tree reversed single linear minimal]
* `-c, --clean`清理环境
* `--custom=CUSTOM` 使用自定义拓扑和节点参数
* `--test=TEST` 测试命令，包括 [cli build pingall pingpair iperf all iperfudp none]
* `-x, --xterms` 在每个节点上打开 xterm
* `--mac` 让MAC 地址跟 DP ID 相同
* `--arp` 配置所有 ARP 项
* `-v VERBOSITY, --verbosity=VERBOSITY [info warning critical error debug output]` 输出日志级别
* `--ip=IP` 远端控制器的IP地址
* `--port=PORT` 远端控制器监听端口
* `--innamespace` 在独立的名字空间内
* `--listenport=LISTENPORT` 被动监听的起始端口
* `--nolistenport` 不使用被动监听端口
* `--pre=PRE` 测试前运行的 CLI 脚本
* `--post=POST` 测试后运行的 CLI 脚本

