## 链路操作
在 Mininet cli 中，使用 `link` 命令，禁用或启用某条链路，格式为
```
link node1 node2 up/down
```

例如临时禁用 s1 跟 h2 之间的链路，可以用
```
link s1 h2 down
```
