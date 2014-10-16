## 自定义拓扑
Mininet 提供了 Python API，可以用来方便的自定义拓扑结构。

在 mininet/custom 目录下给出了几个例子。例如在 topo-2sw-2host.py 文件中定义了一个 mytopo，则可以通过 `--topo` 选项来指定使用这一拓扑，命令为 `sudo mn --custom ~/mininet/custom/topo-2sw-2host.py --topo mytopo --test pingall`。

同样的，我们可以通过下面的 Python 脚本来完成对一个2 层 tree 拓扑网络的测试。

```
from mininet.net import Mininet
from mininet.topolib import TreeTopo
tree4 = TreeTopo(depth=2,fanout=2)
net = Mininet(topo=tree4)
net.start()
h1, h4 = net.hosts[0], net.hosts[3]
print h1.cmd('ping -c1 %s' % h4.IP())
net.stop()
```
