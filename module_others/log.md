## mininet.log 模块
利用 logging 包，主要提供进行 log 相关的功能，包括三个类：MininetLogger、Singleton、StreamHandlerNoNewline。

### mininet.log.MininetLogger
自定义的 logger 类。
提供输出 log、配置 LogLevel 功能。

### mininet.log.Singleton
软件设计模式，限定所创建的类只能有一个实例。供 MininetLogger 使用。

### mininet.log.StreamHandlerNoNewline
自动添加换行和对流进行格式化，供 MininetLogger 使用。
