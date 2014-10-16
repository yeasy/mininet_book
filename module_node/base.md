## 基类

即 mininet.node.Node，
表示一个基本的虚拟网络节点，是所有的网络节点的父类。

实现上其实就是在网络名字空间中的一个shell进程，可以通过各种管道进行通信。该类是模块中其他类的根本，其它类都是直接或间接继承。

节点包括名称、是否在网络名字空间、接口、端口等可能的属性。

### __init__
```
   params: Node parameters (see config() for details)"""

        # Make sure class actually works
        self.checkSetup()

        self.name = name
        self.inNamespace = inNamespace

        # Stash configuration parameters for future reference
        self.params = params

        self.intfs = {}  # dict of port numbers to interfaces
        self.ports = {}  # dict of interfaces to port numbers
                         # replace with Port objects, eventually ?
        self.nameToIntf = {}  # dict of interface names to Intfs

        # Make pylint happy
        ( self.shell, self.execed, self.pid, self.stdin, self.stdout,
            self.lastPid, self.lastCmd, self.pollOut ) = (
                None, None, None, None, None, None, None, None )
        self.waiting = False
        self.readbuf = ''

        # Start command interpreter shell
        self.startShell()
```
初始化函数主要进行参数的初始化，之后通过调用 startShell() 启动一个 shell进程（该进程默认关闭描述符，并从 tty 上分离开来），等待接受传入的命令。句柄被发送给 self.shell 上。

### addIntf
```
def addIntf( self, intf, port=None ):
        """Add an interface.
           intf: interface
           port: port number (optional, typically OpenFlow port number)"""
        if port is None:
            port = self.newPort()
        self.intfs[ port ] = intf
        self.ports[ intf ] = port
        self.nameToIntf[ intf.name ] = intf
        debug( '\n' )
        debug( 'added intf %s:%d to node %s\n' % ( intf, port, self.name ) )
        if self.inNamespace:
            debug( 'moving', intf, 'into namespace for', self.name, '\n' )
            moveIntf( intf.name, self )
```
添加一个接口（比如 `<Intf h1-eth0>` ）到节点上，如果给定了 port（比如 0 ），则建立端口到接口的映射关系。这个映射关系通过 self.intfs 和 self.ports 两个字典来分别维护。

### cmd
该函数能在节点所在的进程shell上执行输入的命令。
```
def cmd( self, *args, **kwargs ):
        """Send a command, wait for output, and return it.
           cmd: string"""
        verbose = kwargs.get( 'verbose', False )
        log = info if verbose else debug
        log( '*** %s : %s\n' % ( self.name, args ) )
        self.sendCmd( *args, **kwargs )
        return self.waitOutput( verbose )
```

### config
配置 MAC，IP 或 default Route 信息。
```
def config( self, mac=None, ip=None,
                defaultRoute=None, lo='up', **_params ):
        """Configure Node according to (optional) parameters:
           mac: MAC address for default interface
           ip: IP address for default interface
           ifconfig: arbitrary interface configuration
           Subclasses should override this method and call
           the parent class's config(**params)"""
        # If we were overriding this method, we would call
        # the superclass config method here as follows:
        # r = Parent.config( **_params )
        r = {}
        self.setParam( r, 'setMAC', mac=mac )
        self.setParam( r, 'setIP', ip=ip )
        self.setParam( r, 'setDefaultRoute', defaultRoute=defaultRoute )
        # This should be examined
        self.cmd( 'ifconfig lo ' + lo )
        return r
```

### connectionsTo
返回所有从自身连接到给定节点的接口，即 [ intf1, intf2... ]。
```
def connectionsTo( self, node):
        "Return [ intf1, intf2... ] for all intfs that connect self to node."
        # We could optimize this if it is important
        connections = []
        for intf in self.intfList():
            link = intf.link
            if link:
                node1, node2 = link.intf1.node, link.intf2.node
                if node1 == self and node2 == node:
                    connections += [ ( intf, link.intf2 ) ]
                elif node1 == node and node2 == self:
                    connections += [ ( intf, link.intf1 ) ]
        return connections
```
