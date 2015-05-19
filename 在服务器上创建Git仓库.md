![alt class='hidden'](https://blog.gintoki.cn/content/images/md_img/git_logo.jpg#thumb)
##1. 为什么要在服务器搭建Git仓库
　GitHub是一个可以称的上完美的代码托管网站，但是免费托管的代码的代价是开源，私有仓库要收取服务费(每个月7$)，我的服务器每个月也才10$...之前在tf上购买了2个主题，正在完善界面和后台，并且我经常在2台电脑上切换使用，Git当然必不可少，因为购买的主题涉及版权问题(我购买后就立马拷贝了几份分享给基友:D)，我不可能放在GitHub开源平台上托管，而私有仓库价格不便宜，于是准备在自己的服务器上搭建Git仓库。如果你有类似需求可以看看本教程。
##2. 搭建Git仓库
###1.1 软件
- Git 最基本的
- Gitosis 公钥管理
- Gitolite 权限控制(我没用过，需要自行Goole)

Gitosis是方便管理团队开发者的密钥，适合大型团队使用，个人和小团队就没必要配置了，很麻烦...我就不讲怎么用了,其实我不会...可以参考[Git服务器Gitosis架设指南](http://blog.csdn.net/king_sundi/article/details/7065525)。

###1.2 安装Git
顺便说下我的服务器操作系统是Centos7，先看看你是否安装过Git。

	$ git --version
若显示版本号说明你已经安装了Git跳过此步骤，若提示找不到git命令请按下面步骤安装

CentOS:
	
	$ yum update -y
	$ yum install git
	
Ubuntu:
	
	$ sudo apt-get install git
	
###1.3 创建git用户及用户组
　为了分离权限等问题，单独创建一个用户来存放你的git仓库，你也可以自己命名用户例如myGit等。

创建git用户和用户组并把git添加到用户组

	$ useradd -g git git

然后给新用户sudo权限,使用visudo命令来编辑/etc/sudoers，找到root	All=(ALL)	ALL这一句,在下面添加git	ALL=(ALL)	ALL，注意空格。

	$ visudo

###1.4 创建git仓库
	$ su git //切换到git用户
	$ cd ~/ //进入用户目录
	$ mkdir testgit.git //仓库名自己取
	$ git init --bare testgit.git //初始化仓库
	$ sudo chown -R git:git testgit.git //给予git用户组下的git用户testgit.git权限，若你在root账户创建的文件夹需要此命令
这样你的git仓库就创建成功了，现在回到本地,试试刚刚创建的仓库。

	$ git clone git@server:/~/testgit.git //server为你的服务器ip或域名
带有端口号的写法

	$ git clone ssh://git@server:port/~/testgit.git //port为你的端口号
然后push试试

	$ cd /testgit.git
	$ echo "test" >> test.txt
	$ git add test.txt
	$ git commit -a -m "test"
	$ git push
或使用三方git工具直接新建仓库，url克隆。</br>
如果遇到错误可能是git用户没有文件夹读写权限问题.修改服务器上仓库权限
　
###1.5 免密码push

　每次push都要输入密码感觉很麻烦,可以在本地生成密钥并上传公共密钥到服务器，会的略过~。

先在本地生成密钥

	$ ssh-keygen -t rsa -P " //-P "表示默认密码为空，也可以不用-P参数，这样就要三车回车，用-P就一次回车
然后在~/.ssh目录下就会生成2个文件id_rsa和id_rsa.pub，id_rsa是私密，不要泄露，然后把公钥id_rsa.pub上传到服务器，可以使用scp命令：

	$ scp id_rsa.pub git@server:~/.ssh/
id_rsa.pub是你的公钥路径，git是你刚刚创建的用户名，如果提示找不到路径请在服务器git用户目录下手动创建文件夹。</br>
登录git用户:

	$ cd ~/
	$ mkdir .ssh
	$ chmod 700 .ssh //.ssh权限必须为700
上传完成后:

	$ cd ~/.ssh/
	$ cat id_rsa.pub >> authorized_keys
	$ chmod 600 authorized_keys //authorized_keys权限必须为600
设置完后就可以免密码push了，同样ssh登录也不需要密码。

###1.6 禁用shell登录
　如果你是小组开发，并且每个人都上传了公钥到authorized_keys里，意味着每个人都可以登录你得服务器，为了安全起见可以禁用shell登录。
	
	$ sudo vim /etc/passwd
找到git:git:1001:1001::/home/git:/bin/bash</br>
改成git:git:1001:1001::/home/git:/usr/bin/git-shell

我用的是日本linode服务器，我测试过clone一个27m的项目只用了5秒左右，比起GitHub快了不少:) 
	