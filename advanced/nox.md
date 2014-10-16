## 使用 NOX

首先确定没有其他控制器在运行（占据 6633 端口）
```
sudo killall controller
```
启动 Mininet
```
sudo mn --topo single,3 --mac --switch ovsk --controller remote
```
然后启动 NOX，默认路径为 ~/noxcore/build/src，重新打开一个 ssh 终端执行
```
./nox_core -v -i ptcp: pytutorial
```
会自动打开运行 tutorial 应用的 NOX，打印出详细的调试信息，并监听 6633 端口。

直到打印出类似如下信息，说明交换机已经成功连接到 NOX。
```
00039|nox|DBG:Registering switch with DPID = 1
```
通过互 ping 测试，各个主机连通，此时 switch 等同于一个 hub。
然后通过修改 ~/noxcore/src/nox/coreapps/tutorial/pytutorial.py 中代码，让 NOX 工作成一个带学习功能的交换机。相关命令参考 ofinclude 代码，以及 NOX 对各个包的解析代码目录：~/noxcore/src/nox/lib/packet/。

通过编写 NOX 程序，我们可以让交换机的行为更加智能化、复杂化。为了测试我们编写的 NOX 程序，我们可以使用 cbench 来进行测试。

