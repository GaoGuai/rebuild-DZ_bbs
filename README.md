DZ论坛重建  将原来的数据迁移到新的DZ论坛
=====
先说明一下我遇到的问题
一开始建站，考虑的并不全面，不管是从安全方面还是服务器运行的性能上面，都是需要优化的，事情拖延了很长时间，就在昨天真的决定要好好整理下DZ的论坛了

要重新建站，不能急，因为我论坛的数据一定要保证好，所以我就一直在本地测试各种方法，下面就记录一下我重新建站的过程

1. 备份数据库
-------
在DZ论坛的管理中心->站长->数据库->备份,在数据备份类型里面选择：`Discuz! 和 UCenter 数据`
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/数据库备份.png)

2. 网站备份
-------
以防你中间的过程出现任何的意外，将服务器中的网站原始文件全部拷贝下来，我是用FTP将整个网站下载到本地的，同时也将备份的数据库下载下来。

3. 下载DZ程序
-------
这里下载的DZ程序是网站重新安装用的，而且为了防止出错，下载的DZ程序要和原来的DZ论坛版本一模一样，包括版本和编码方式，我用的DZ3.2的GBK编码方式，这里是下载地址 http://download.comsenz.com/DiscuzX/3.2/Discuz_X3.2_SC_GBK.zip 如果你不知道你的DZ版本和编码方式，那你可以在你论坛页面的左下角看到查看到论坛的版本，并且可以通过在论坛页面中 “查看网页源代码” 第四行里面有源码的编码方式。</br>
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/查看编码方式.png)
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/查看版本.png)

4. 选择服务器
-------
综合安全和服务器性能，我决定这次不适用Windows系统了，改用了阿里的Linux系统，使用的是CentOS 7.6操作系统

5. 安装宝塔程序
-------
然后使用的宝塔web管理，CentOS 7的宝塔安装代码是 
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
不管你用什么工具连接服务器，运行上面的代码，会提示安装，输入“y”，就会帮你安装好宝塔了，在安装结束后，请记住生成的信息，里面包含了你进入宝塔界面的链接和需要登录的用户名和密码，为了安全起见，请在登录后立马修改相关内容。
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/修改宝塔信息.png)

6. 修改端口
-------
然后发现使用宝塔需要打开几个常用端口，为了安全起见，我把常用的端口在宝塔Web界面中都修改了，并且在阿里控制台也都把相应的端口都修改了，在这里也建议大家都把端口都修改了。PS：如果你服务器是阿里、腾讯或者华为之类的话，你需要再相应的控制台把宝塔需要的端口打开，可以不修改
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/端口修改.png)

7. 安装操作环境
-------
在web宝塔操作界面，软件商店->运行环境安装下面几个软件
Nginx 1.16.0    MySQL 5.5.62   PHP-5.6    phpMyAdmin 4.4    Pure-Ftpd 1.0.49

8. 新建数据库
-------
输入新建的数据库的名称，登录名和登录密码，密码尽量复杂。在选择编码方式时，请选择和论坛相同的编码方式，我论坛的编码方式是GBK，所以我选择的是GBK编码方式
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/新建数据库.png)

9. 建立网站
-------
按照相应的提示信息进行输入，如果没有域名，那就直接输入服务器IP地址
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/新建网站.png)

10. 添加FTP
-------
添加FTP，输入任意的用户名和密码，但是根目录一定要选择建立网站时生成的目录。
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/添加FTP.png)
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/根目录.png)

11. 上传DZ程序
-------
将之前从官网下载的DZ源码程序解压，将里面的upload文件夹里面的所有的文件通过FTP上传到建立网站的根目录

12. 安装DZ程序
-------
通过域名直接访问，或者通过IP来访问，会弹出安装DZ程序界面。如果有乱码情况，那是因为服务器PHP解码方式不对，可以在PHP的配置文件中修改。我是将默认UTF-8编码修改成GBK编码。然后正常安装就好了，之后填写的信息就是上面数据库之类的信息。我已经弄好了，不能截图了。有一点要注意建表的前缀要和之前论坛的一样，如果你忘记了，那就去数据库看一下，又或者在备份文件里面看一下都行。
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/GBK.png)

13. 恢复数据库
-------
安装结束后，将之前备份的数据库和DZ源码中的Discuz_X3.2_SC_GBK\utility\restore.php上传到服务器的网站根目录下data目录下。进入论坛管理中心->站长->数据库->恢复 页面下直接恢复数据。
![](https://github.com/GaoGuai/rebuild-DZ_bbs/blob/master/images/恢复数据库.png)

14. 上传相关文件
-------
先删除data/restore.php，防止自己遗忘后被人利用这个页面。上传下面说的这几个文件夹，记住，是文件夹，是文件夹，是文件夹
备份的文件夹\data\addonmd5
备份的文件夹\data\attachment
备份的文件夹\uc_server\images
备份的文件夹uc_server\plugin
备份的文件夹\old\template

到这里基本上就结束了，如果有哪里有问题，欢迎提问指出。
电报频道：https://t.me/jiandandian_chanel
论坛：www.jiandandian.online
个人QQ：2367361478，有问题加我，请勿骚扰。


