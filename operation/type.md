## 指定交换机跟控制器类型
通过 `--switch` 选项跟 `--controller` 选项可以分别指定采用哪种类型的交换机跟控制器。

例如使用用户态的交换机：
```
sudo mn --switch user
```
使用 OpenvSwitch：
```
sudo mn --switch ovsk
```
使用 NOX pyswitch：
* 首先确保 NOX 运行
```
cd $NOX_CORE_DIR
./nox_core -v -i ptcp:
```
然后 `Ctrl-c` 杀死 NOX 进程
* 然后指定 NOX 交换机
```
sudo -E mn --controller nox_pysw
```

注意：通过`-E`选项来保持预定义的环境变量（此处为 `NOX_CORE_DIR`）。
