## mininet.link.Link
表示基本的一条链路，最基本的链路在 mininet 中其实就是一对 veth 接口对。
```
def __init__( self, node1, node2, port1=None, port2=None,
                  intfName1=None, intfName2=None,
                  intf=Intf, cls1=None, cls2=None, params1=None,
                  params2=None ):
        """Create veth link to another node, making two new interfaces.
           node1: first node
           node2: second node
           port1: node1 port number (optional)
           port2: node2 port number (optional)
           intf: default interface class/constructor
           cls1, cls2: optional interface-specific constructors
           intfName1: node1 interface name (optional)
           intfName2: node2  interface name (optional)
           params1: parameters for interface 1
           params2: parameters for interface 2"""
        # This is a bit awkward; it seems that having everything in
        # params would be more orthogonal, but being able to specify
        # in-line arguments is more convenient!
        if port1 is None:
            port1 = node1.newPort()
        if port2 is None:
            port2 = node2.newPort()
        if not intfName1:
            intfName1 = self.intfName( node1, port1 )
        if not intfName2:
            intfName2 = self.intfName( node2, port2 )

        self.makeIntfPair( intfName1, intfName2 )

        if not cls1:
            cls1 = intf
        if not cls2:
            cls2 = intf
        if not params1:
            params1 = {}
        if not params2:
            params2 = {}

        intf1 = cls1( name=intfName1, node=node1, port=port1,
                      link=self, **params1  )
        intf2 = cls2( name=intfName2, node=node2, port=port2,
                      link=self, **params2 )

        # All we are is dust in the wind, and our two interfaces
        self.intf1, self.intf2 = intf1, intf2
```
创建链路时，需要在两个节点上分别生成两个端口，利用节点和端口，获取对应的两个网络接口的名称，例如 s1-eth0 和 h1-eth0，然后调用 makeIntfPair() 方法，最终调用 util.py 中的 makeIntfPair() 方法，调用系统中的 `ip link` 命令来创造一对 veth pair。
```
def makeIntfPair( intf1, intf2 ):
    """Make a veth pair connecting intf1 and intf2.
       intf1: string, interface
       intf2: string, interface
       returns: success boolean"""
    # Delete any old interfaces with the same names
    quietRun( 'ip link del ' + intf1 )
    quietRun( 'ip link del ' + intf2 )
    # Create new pair
    cmd = 'ip link add name ' + intf1 + ' type veth peer name ' + intf2
    return quietRun( cmd )
```
