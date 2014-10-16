## mininet.topo.Topo
拓扑基类，默认的拓扑图被 multigraph 类维护，此外还包括节点、连接信息等。主要的方法就是添加节点、连接等。
Topo 中一个 node 实际上就是图结构中的一个节点，一个 port 是全局维护增长的源和目的 node 所对应的序号，而连接
### __init__
```
def __init__(self, hopts=None, sopts=None, lopts=None):
        """Topo object:
           hinfo: default host options
           sopts: default switch options
           lopts: default link options"""
        self.g = MultiGraph()
        self.node_info = {}
        self.link_info = {}  # (src, dst) tuples hash to EdgeInfo objects
        self.hopts = {} if hopts is None else hopts
        self.sopts = {} if sopts is None else sopts
        self.lopts = {} if lopts is None else lopts
        self.ports = {}  # ports[src][dst] is port on src that connects to dst
```
### addNode
```
def addNode(self, name, **opts):
        """Add Node to graph.
           name: name
           opts: node options
           returns: node name"""
        self.g.add_node(name)
        self.node_info[name] = opts
        return name
```
添加节点方法被添加主机 addHost、交换机 addSwitch、控制器 addController 等方法使用。

该方法在图上添加一个节点，然后添加对应的节点信息到拓扑的参数上。
### addPort
```
def addPort(self, src, dst, sport=None, dport=None):
        '''Generate port mapping for new edge.
        @param src source switch name
        @param dst destination switch name
        '''
        self.ports.setdefault(src, {})
        self.ports.setdefault(dst, {})
        # New port: number of outlinks + base
        src_base = 1 if self.isSwitch(src) else 0
        dst_base = 1 if self.isSwitch(dst) else 0
        if sport is None:
            sport = len(self.ports[src]) + src_base
        if dport is None:
            dport = len(self.ports[dst]) + dst_base
        self.ports[src][dst] = sport
        self.ports[dst][src] = dport
```
addPort 会同时创建源和目标节点上的端口号信息。
拓扑中所有的 port 都被 self.ports 结构维护，其中 ports[src][dst] 表示在 src 节点上的 port，该 port 所在 link 连接到 dst 节点。
添加一个 port 就是更新了这些信息。
### addLink
```
def addLink(self, node1, node2, port1=None, port2=None,
                **opts):
        """node1, node2: nodes to link together
           port1, port2: ports (optional)
           opts: link options (optional)
           returns: link info key"""
        if not opts and self.lopts:
            opts = self.lopts
        self.addPort(node1, node2, port1, port2)
        key = tuple(self.sorted([node1, node2]))
        self.link_info[key] = opts
        self.g.add_edge(*key)
        return key
```
添加一条连接实际上就是添加对应的两个 port，并在图上添加上边。
