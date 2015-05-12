![alt class='hidden'](https://blog.gintoki.cn/content/images/md_img/ssl_head.jpg#thumb)

##1. 什么是 SSL 证书？
![alt=''](https://blog.gintoki.cn/content/images/md_img/ssl_title.jpg)
　SSL，英文全称为Secure Sockets Layer ，直译为“安全套接层”。SSL及其继任者传输层安全（Transport Layer Security，TLS）是为网络通信提供安全及数据完整性的一种安全协议。TLS与SSL在传输层对网络连接进行加密。

　SSL 证书提供了一种在互联网上身份验证的方式,是用来标识和证明通信双方身份的数字信息文件。使用 SSL 证书的网站，可以保证用户和服务器间信息交换的保密性，具有不可窃听、不可更改、不可否认、不可冒充的功能。SSL证书由权威认证机构（CA）颁发。Entrust 正是全球知名 CA 。中国大多数金融行业网站正在使用 ssl证书。
  
　网络已经成为人们生活中不可缺少的一部分，相对于在街头漫步、传统购物，如今的人们，更习惯在网络上进行消费。然而，钓鱼网站、盗号木马、信息拦截、资料泄露等等层出不穷的网络犯罪警示我们：在享受便利的同时，您的网站正面临将信息完全暴露在互联网上的风险。而通过 SSL 证书，在网友的计算机和正在查看的网站间提供一个加密通道，防止第三方干预通过该通道传输的信息。
##2. 申请并配置 SSL 证书 
###2.1 申请免费的 ssl 证书
打开[沃通免费SSL](http://www.wosign.com/products/free_ssl.htm)页面。点击立即购买。
　![alt=''](https://blog.gintoki.cn/content/images/md_img/ssl1.png)
　填写你的网站信息，首先填写你的域名然后在第二部里点击立即验证并选择你的邮箱，用来接受邮件验证你的域名。
　![alt=''](https://blog.gintoki.cn/content/images/md_img/ssl4.png)
　之后填写完后面的信息，提交申请。
　![alt=''](https://blog.gintoki.cn/content/images/md_img/ssl3.png)
　然后就可以等待沃通审核了，大概1天时间，注意你的邮箱，审核通过侯会邮件通知。</br>
　审核通过侯就可以登录沃通或直接通过邮件链接下载你的 SSL 证书。默认下载的是一个压缩包文件解压需要密码就是你注册时所填写的证书保护密码。解压后有5个服务器版本的压缩包里面放置了对应的 crt 证书和 key。我用的是 nginx 服务器，其他版本的服务器可以参考沃通[SSL证书安装指南](http://www.wosign.com/support/ssl_installation.htm)。
###2.2 配置 nginx
　
上传 for Nginx.zip到你的 linux 服务器nginx 目录下,我linux 操作系统是 centos7路径为:/etc/nginx/conf.d然后解压。

	cd /etc/nginx/conf.d/
	uzip for Nginx.zip
然后编辑网站配置文件配置文件

	vim /etc/nginx/conf.d/example.conf //这个路径换成你的网站配置文件路径
	
	server {
    listen       443; //监听 https 的端口号
    server_name  www.example.com; //域名
    
    ssl on; //开启 ssl
    ssl_certificate /etc/nginx/conf.d/example.crt; //指向你的证书路径
    ssl_certificate_key /etc/nginx/conf.d/example.key; //指向你的 key 路径
    location / {
        root   /var/www/example; //指向你的网站目录
        index  index.html index.htm; //默认打开页面文件
    }
	server{
		listen      80; //监听80端口
    	server_name www.example.com; //域名和上面一样
    	rewrite ^/(.*) https://$server_name$1 permanent;//指向https
	}
最后重启你的 nginx 服务器打开你的网页试试
![alt=''](https://blog.gintoki.cn/content/images/md_img/ssl5.png)
　用 chrome 打开网站可以看到域名前的绿色小锁，点开后能看到你的证书信息，大功告成！
不过使用的 ssl 后网站加载的速度明显变慢了很多，不过为了网站的安全性还是值得的。
##3. 服务器装上 SSL 证书会不会影响到速度和流量？
　使用 ssl 会增加服务器CPU的处理负担，因为要为每一个SSL连接实现加密和解密，但一般不会影响太大，因为只是在服务端和客户端建立SSL通道初始阶段速度会稍显慢，但一旦SSL通道建立后速度基本就不会有任何影响了。同时建议注意以下几点以减轻服务器的负担：

- 仅为需要加密的页面使用SSL，不要把所有页面都使用https，特别是访问量最大的首页。
- 尽量不要在使用了SSL的页面上设计大块的图片文件和其他大文件，尽量使用简洁的文字页面。
- 如果网站的访问量非常大，则建议另外购买SSL加速卡来专门负责SSL加解密工作，可以完全不增加服务器任何负担，或另外增加服务器。
