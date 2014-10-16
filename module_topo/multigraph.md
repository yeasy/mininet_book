## mininet.topo.MultiGraph
表示一个图结构。
类似于networkx中的图G(V,E)的概念。主要维护节点、边信息。
在MultiGraph中，节点就是一个序号，边则通过节点和节点所对应的连接列表中元素来表示。节点和节点的连接列表的对应关系通过字典结构来维护。

### __init__
```
def __init__( self ):
        self.data = {}
```
图结构最主要的功能就是维护一个字典。Key 是节点，value 是该节点所连接的所有的其他节点的列表。
```
add_node
    def add_node( self, node ):
        "Add node to graph"
        self.data.setdefault( node, [] )
```
添加一个节点，实际上就是添加一个 key 到 data 字典中。
```
add_edge
    def add_edge( self, src, dest ):
        "Add edge to graph"
        src, dest = sorted( ( src, dest ) )
        self.add_node( src )
        self.add_node( dest )
        self.data[ src ].append( dest )
```
添加一条边，实际上就是添加两个节点，然后将连接信息放到 data 字典中（需要注意的是一条边的信息仅被保存了一次，即放到序号较小的节点对应的 list 中）。
