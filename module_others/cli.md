## mininet.cli 模块
主要包括 CLI 类，该类继承自 Python 库的 Cmd 类。

提供对 CLI 的支持，创建 Mininet 的 bash，接受通过 bash 传输的 Mininet 命令，形成可以进行交互的 Mininet 命令行环境。

主要方法包括初始化之后提供一个界面，通过 Python 库的 Cmd 类的 cmdloop() 方法不断执行输入的命令。这些命令可以是指定对某个节点进行的操作或者是对 Mininet 对象本身。

对于大部分对 Mininet 对象的操作命令 xxx，会调用 Python 库的 Cmd 类的 onecmd() 方法来执行，该方法会对应调用 do_xxx 方法。

各个 do_xxx 方法分别用于执行支持的命令。例如 do_dpctl() 方法响应用户输入 dpctl 相关命令。目前包括 dpctl，dump，EOF，exit，gterm，help，intfs，iperf，iperfudp，link，net，nodes，noecho，pingall，pingallfull，pingpair，pingparifull，px，py，quit，sh，source，time，x，xterm 等。
