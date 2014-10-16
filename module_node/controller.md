## 控制器类
### mininet.node.Controller
控制器基类。默认的控制器是一个参考的实现，controller。

表示一个控制器节点。包括 IP 地址、端口等。

主要方法包括启动和停止一个控制器。

#### __init__
```
def __init__( self, name, inNamespace=False, command='controller',
                  cargs='-v ptcp:%d', cdir=None, ip="127.0.0.1",
                  port=6633, **params ):
        self.command = command
        self.cargs = cargs
        self.cdir = cdir
        self.ip = ip
        self.port = port
        Node.__init__( self, name, inNamespace=inNamespace,
                       ip=ip, **params  )
        self.cmd( 'ifconfig lo up' )  # Shouldn't be necessary
        self.checkListening()
```
#### checkListening
确保系统中安装了 telnet，并且在监听端口上并没有其他控制器在监听。

#### start
```
def start( self ):
        """Start <controller> <args> on controller.
           Log to /tmp/cN.log"""
        pathCheck( self.command )
        cout = '/tmp/' + self.name + '.log'
        if self.cdir is not None:
            self.cmd( 'cd ' + self.cdir )
        self.cmd( self.command + ' ' + self.cargs % self.port +
                  ' 1>' + cout + ' 2>' + cout + '&' )
        self.execed = False
```
该方法检查控制器程序存在，并根据传入的参数来启动它。

#### stop
```
def stop( self ):
        "Stop controller."
        self.cmd( 'kill %' + self.command )
        self.terminate()
```
该方法杀死控制器进程和节点的 shell 进程，并执行清理工作。

### mininet.node.NOX
表示一个 NOX 控制器（需要系统中事先安装了 NOX）。

### mininet.node.OVSController
表示一个ovs-controller（需要系统中实现安装了 ovs-controller）。

### mininet.node.RemoteController
表示一个在 Mininet 控制外的控制器，即用户自己额外运行了控制器，此处需要维护连接的相关信息。

