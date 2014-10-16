## 主机类
包括 Host 和 CPULimitedHost 两个类。

### mininet.node.Host
表示一个主机节点，目前跟 Node 类定义相同。
在主机类上执行命令可以通过 Cmd() 或者 sendCmd() 方法，前者会等待命令的输出结果，后者会直接返回，并允许使用后续的 monitor() 来进行监视跟踪。

### mininet.node.CPULimitedHost
继承自 Host 类，通过 cgroup 工具来对 CPU 进行限制。

#### __init__
```
def __init__( self, name, sched='cfs', **kwargs ):
        Host.__init__( self, name, **kwargs )
        # Initialize class if necessary
        if not CPULimitedHost.inited:
            CPULimitedHost.init()
        # Create a cgroup and move shell into it
        self.cgroup = 'cpu,cpuacct,cpuset:/' + self.name
        errFail( 'cgcreate -g ' + self.cgroup )
        # We don't add ourselves to a cpuset because you must
        # specify the cpu and memory placement first
        errFail( 'cgclassify -g cpu,cpuacct:/%s %s' % ( self.name, self.pid ) )
        # BL: Setting the correct period/quota is tricky, particularly
        # for RT. RT allows very small quotas, but the overhead
        # seems to be high. CFS has a mininimum quota of 1 ms, but
        # still does better with larger period values.
        self.period_us = kwargs.get( 'period_us', 100000 )
        self.sched = sched
        self.rtprio = 20
```
