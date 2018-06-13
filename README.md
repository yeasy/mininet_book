Mininet 应用与源码剖析
============
[Mininet](http://mininet.org) 是研究软件定义网络，进行快速验证的高效模拟平台。

本书的一到三章介绍 Mininet 的安装和使用；第四章介绍一些高级功能；五到七章分析 Mininet 的源码实现。

最新版本在线阅读：[GitBook](https://www.gitbooks.io/book/yeasy/mininet_book)。

本书源码在 Github 上维护，欢迎参与： [https://github.com/yeasy/mininet_book](https://github.com/yeasy/mininet_book)。

感谢所有的 [贡献者](https://github.com/yeasy/mininet_book/graphs/contributors)。

## 更新历史:

* 0.6: 2013-12-16
    * 完善对 topo 模块、net 模块等的分析。
* 0.5: 2013-12-11
    * 补充对部分 example 文件的分析；
    * 增加对 clean 模块的分析。
* 0.4: 2013-11-18
	* 补充对 link 和 node 库的核心代码分析；
    补 充运行文件分析。
* 0.3: 2013-11-16
	* 完成运行文件分析。
* 0.2: 2013-11-15
	* 完成库文件分析。
* 0.1: 2013-10-11
	* 完成代码结构分析。

## 参加步骤
* 在 GitHub 上 `fork` 到自己的仓库，如 `user/mininet_book`，然后 `clone` 到本地，并设置用户信息。
```
$ git clone git@github.com:user/mininet_book.git
$ cd mininet_book
$ git config user.name "User"
$ git config user.email user@email.com
```
* 修改代码后提交，并推送到自己的仓库。
```
$ #do some change on the content
$ git commit -am "Fix issue #1: change helo to hello"
$ git push
```
* 在 GitHub 网站上提交 pull request。
* 定期使用项目仓库内容更新自己仓库内容。
```
$ git remote add upstream https://github.com/yeasy/mininet_book
$ git fetch upstream
$ git checkout master
$ git rebase upstream/master
$ git push -f origin master
