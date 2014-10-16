## mininet.clean 模块
提供对执行 Mininet 后的清理工作，主要包括 cleanup() 函数，该函数实际上调用了 sh() 函数。

cleanup() 函数主要包括清除僵尸进程，临时文件，X11 tunnel，额外的内核态 datapath，ovs datapath，ip link 等。

实现过程主要是通过调用 subprocess 模块（主要用于执行外部命令和程序）中的 Popen 类中方法来对进程发送指令。
```
def sh( cmd ):
    "Print a command and send it to the shell"
    info( cmd + '\n' )
    return Popen( [ '/bin/sh', '-c', cmd ], stdout=PIPE ).communicate()[ 0 ]
```
communicate() 是 Popen 对象的一个方法，该方法会阻塞父进程，直到子进程完成。
通过指定 stdout=PIPE，可以通过 stdout 获取程序的返回值。通过列表传入要执行的命令和参数。
