## mininet.link.Intf
表示基本的网络接口，比如 h1-eth0 表示 host 1 上的 eth0 接口。
属性包括所在的节点，名称，所接的 link，mac/ip 信息等。
构造的时候会传入节点、端口等属性，并绑定接口到对应的节点的端口上。
```
def __init__( self, name, node=None, port=None, link=None, **params ):
        """name: interface name (e.g. h1-eth0)
           node: owning node (where this intf most likely lives)
           link: parent link if we're part of a link
           other arguments are passed to config()"""
        self.node = node
        self.name = name
        self.link = link
        self.mac, self.ip, self.prefixLen = None, None, None
        # Add to node (and move ourselves if necessary )
        node.addIntf( self, port=port )
        # Save params for future reference
        self.params = params
        self.config( **params )
```
所支持的方法包括配置 mac/ip 等配置方法，大都是通过 ifconfig 命令在对应节点上调用cmd方法来实现。
此外，还提供了 config() 方法来一次性配置所有的属性。
