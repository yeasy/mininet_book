## 查看信息

查看全部节点：
```
mininet> nodes
available nodes are:
c0 h2 h3 s1
```
查看链路信息：
```
mininet> net
s1 <-> h2-eth0 h3-eth0
```
输出各节点的信息：
```
mininet> dump
c0: IP=127.0.0.1 intfs= pid=1679
s1: IP=None intfs=s1-eth1,s1-eth2 pid=1682
h2: IP=10.0.0.2 intfs=h2-eth0 pid=1680
h3: IP=10.0.0.3 intfs=h3-eth0 pid=1681
```
