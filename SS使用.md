##Shadowsocks使用方法

###1.1软件下载

　需要新版本的可以去官方地址下载，要嫌麻烦就直接用我提供的地址下载，但我可能不会及时更新到最新版。若部分地址失效请在下方留言或email我。

- [官方下载地址](https://shadowsocks.com/client.html)
- [Windows版](http://aboutme.gintoki.cn/download/Shadowsocks-win-2.3.1.zip)
- [MAC版](http://aboutme.gintoki.cn/download/ShadowsocksX-2.6.3.dmg)
- [Android2.6.7去广告版](http://aboutme.gintoki.cn/download/Signed_Shadowsocks_v2.6.7_Modified.Kane.NoAD.apk)
- ios非越狱用户（[摸我下载](https://itunes.apple.com/us/app/shadowsocks/id665729974?ls=1&mt=8)）
- ios越狱用户在cydia里搜索Shadowsocks并安装，若搜索不到请添加源([摸我看如何添加](http://jingyan.baidu.com/article/2f9b480d5e1bdf41cb6cc213.html))


其他用户请去官方下载地址下载

###1.2配置
####1.2.1 Windows版配置

- 解压Shadowsocks-win-2.3.1.zip
- 运行Shadowsocks-win-2.3.1.exe

1）任务栏右下角(如下图所示)对着那个纸飞机右键，服务器>编辑服务器 
![alt](https://blog.gintoki.cn/content/images/md_img/ss_win1.jpg)

2）接着点击添加，分别填入服务器ip、服务器端口、密码、加密方式，备注就是保存后显示在右边列表中的名称，不填的话默认使用ip作为名称。然后点确定。

![alt](https://blog.gintoki.cn/content/images/md_img/ss_win2.jpg)

3）选择代理模式，右键纸飞机>系统代理模式。windwos用户推荐使用PAC模式，你也可以选择全局模式，但是windows版客户端容易崩溃(更新了很多版本一直没有解决)。

4）启动代理，右键纸飞机选择第一项启动系统代理，若前面打勾说明已经启动再次点击可取消启动。
####1.2.2 MAC版配置
配置方法参考Windows，附上图片，推荐自动代理模式

![alt](https://blog.gintoki.cn/content/images/md_img/ss_mac1.jpg)

![alt](https://blog.gintoki.cn/content/images/md_img/ss_mac2.jpg)

####1.2.3 Adnroid版配置
打开软件，已root过的给予权限，没root会以vpn方式启。配置如下图

![alt](https://blog.gintoki.cn/content/images/md_img/ss_android1.jpg)

####1.2.4 IOS版配置
非越狱用户：

这是个自带SS的浏览器，只能通过这个浏览器来使用代理服务，不是全局代理，所以其他软件或其他浏览器都不能使用代理。

![alt](https://blog.gintoki.cn/content/images/md_img/ss_ios1.png)

越狱用户：

![alt](https://blog.gintoki.cn/content/images/md_img/ss_ios2.jpg)


其他用户自己参照上面例子设置，若有疑问欢迎QQ联系我，想了解如何在服务器上搭建shadowsocks，请参考Cheney的博文【[Shadowsocks的配置与优化](https://www.yangchengyu.net/2015/05/10/linux-shadowsocks/)】

q:382723500

最后提供我的免费ss服务，[点我进入](http://sspanel.gintoki.cn)。注册需要邀请码，加我q向我索取邀请码，免费名额有限先到先得。
