ABOUT
=====
bcloud 是[百度网盘](http://pan.baidu.com)的Linux桌面客户端实现.

支持的系统版本:

* Fedora 20
* Debian sid
* Debian testing
* Debian stable
* Ubuntu 14.04
* Ubuntu 13.10
* Ubuntu 12.04
* OpenSuse 13

安装
====
请用户直接到 [bcloud-packages](https://github.com/LiuLang/bcloud-packages)
下载发行版相对应的安装包, 比如deb, rpm等.

如果需要手动安装的话, 也可以用pip3来安装, 比如: `# pip3 install bcloud`

如果不想安装安装, 请至少把blcoud/share目录合并到~/.local/share, 不然图标会显示不全.

DEPENDENCIES
===========

* python3-gi  Gtk3 的python3 绑定. 这个包需要手动安装gir1.2-gtk-3.0, 但它并
没有把这个依赖关系写清楚, 详细情况请看 [issue 5](https://github.com/LiuLang/bcloud/issues/5)
* python3-urllib3 urllib的封装, 更易用, 在这里 https://pypi.python.org/pypi/urllib3.
* gnome-icon-theme-symbolic Gnome3 提供的一套按纽.
* python3-keyring  这个模块是推荐安装的, 用于把帐户的密码存放到
gnome-keyring或kwallet里面; 如果缺少了这个模块, 帐户的密码就会被明文存储!
* gir1.2-notify 这个是GtkNotification的接口, 显示桌面消息通知

Q&A
===
1. 为什么bcloud不支持本地与远程服务器同步?

因为百度网盘没有公开它的同步算法.

2. 为什么上传时的进度条移动的很慢?

因为在上传大文件时, 根据情况, 可能会使用分片上传功能--把文件分成若干份, 每次
只上传一部分--这种功能可以实现断点续传. 目前bcloud里面支持对文件进行分片的单
位是1MB~5MB, 默认是1MB, 即每次上传1MB. 百度网盘对一个大文件的分片个数做了限
制, 最多只能有1024个分片. 所以, bcloud支持上传的单个文件最大值是1024GB~5120GB.
在上传这个分片过程中如果出错, 这个分片就会被丢弃, 在下次继续上传时, 只需要
重新上传这个分片就可以了. 当所有分片都上传完成后, 在服务器上把这些分片合并
成一个完整的大文件.
在"首选项"里可以指定分片的大小.

3. 为什么有时候关闭窗口时无响应?

这个是因为后台的HTTP请求线程没响应, 一直卡在那里. 现在还没找到一个合适的方式
来处理未响应的后台线程; 使用线程池/进程池等方法感觉没有必要, 这样会把bcloud
搞的很复杂.

4. 能不能支持其它网盘?

我本人时间和精力都非常有限, 单单开发bcloud就占用了我一个多月的业余时间. 而且
本来工作之外的时间就非常少, 还有很多其它事情要处理. 所以如果你报告了bug或者
反馈了问题, 没有及时收到回复, 请多等待一下, 我会安排时间处理这些问题的.



COPYRIGHT
========
Copyright (C) 2014 [LiuLang](mailto:gsushzhsosgsu@gmail.com)

基于GNU通用许可协议第三版发布, 详细的许可信息请参考 [LICENSE](LICENSE)

SCREENSHOTS
==========
![MainWindow](screenshots/bcloud.png)
