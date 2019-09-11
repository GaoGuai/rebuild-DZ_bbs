DZ论坛重建  将原来的数据迁移到新的DZ论坛
=====
先说明一下我遇到的问题
一开始建站，考虑的并不全面，不管是从安全方面还是服务器运行的性能上面，都是需要优化的，事情拖延了很长时间，就在昨天真的决定要好好整理下DZ的论坛了

要重新建站，不能急，因为我论坛的数据一定要保证好，所以我就一直在本地测试各种方法，下面就记录一下我重新建站的过程

1. 备份数据库
在DZ论坛的管理中心->站长->数据库->备份,在数据备份类型里面选择：Discuz! 和 UCenter 数据
2. 网站备份
以防你中间的过程出现任何的意外，将服务器中的网站原始文件全部拷贝下来，我是用FTP将整个网站下载到本地的
3. 下载DZ程序
这里下载的DZ程序是网站重新安装用的，而且为了防止出错，下载的DZ程序要和原来的DZ论坛版本一模一样，包括版本和编码方式，我用的DZ3.2的GBK编码方式，这里是下载地址 http://download.comsenz.com/DiscuzX/3.2/Discuz_X3.2_SC_GBK.zip 如果你不知道你的DZ版本和编码方式，那你可以在你论坛页面的左下角看到查看到论坛的版本，并且可以通过在论坛页面中 “查看网页源代码” 第四行里面有源码的编码方式。
