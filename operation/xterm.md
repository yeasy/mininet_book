## 使用XTerm
为了能够正确使用 xterm，我们需要做些准备工作。在这里推荐利用远程方式登录到 OpenflowVM。

### 客户端
对于自带 X 的 Linux 主机，无需配置 X。

如果客户端是 Windows 主机，需要先在 Windows 机器上安装 Xserver（Xming）。下载地址：http://sourceforge.net/projects/xming/files/Xming/6.9.0.31/Xming-6-9-0-31-setup.exe。

如果你使用 secureCRT 远程登录到 OpenflowVM，需要在“会话选项->SSH2->密钥交换”下，取消 `diffie-hellman-group14` 和 `diffie-hellman` 选择；同时在“远程/X11”下，选择转发“X11数据包（F）”；点击确定。

开启 Xming，使用如下命令远程到Openflow VM即可。
```
ssh -X openflow@[Guest IP here]
```
如果你使用 puTTY 远程登录到 OpenflowVM:
点击“puTTY->Connection->SSH->X11”，选择“X11 forwarding->Enable X11 forwaring”；开启 Xming，点击 Windows 开始按钮，在运行栏输入“cmd”，打开终端，输入 `cd <dir>` 切换到保存 puTTY 的目录下；使用下面的命令远程登录到 openflow VM。
```
putty.exe -X openflow@[Guest IP here]
```

### 主机端
通过使用 `-x` 参数，Mininet 在启动后会在每个节点上自动打开一个 XTerm，方便某些情况下的对多个节点分别进行操作。命令为
```
sudo mn -x
```
在进入 mn cli之后，也可以使用 xterm node 命令指定启动某些节点上的 xterm，例如分别启用 s1 跟 h2 上的 xterm，可以用
```
xterm s1 h2
```
