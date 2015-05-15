　昨天一直用iTerm运行Python ...我也是醉了，今天分别在sublime Text和Pycharm上体验了下。</br>
　Sublime Text编写python简单易用，适合我这种初学新手，但是遇到点棘手的地方，Sublime Text 运行带有 raw_input 的时候莫名其妙的报错，google了下发现Sublime Text Command+b 运行Python控制台不支持输入，于是继续google,找到一款插件[SublimeREPL](https://github.com/wuub/SublimeREPL)，安装方法:
　
###1. 为Sublime Text添加Installed Packages
若已经安装略过
#### 使用Ctrl+`快捷键或者通过View > Show Console菜单打开命令行复制下面代码输入
	
	import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
![alt='图片失效刷新重试'](https://blog.gintoki.cn/content/images/md_img/py_sublime%20text1.jpg)

![alt='图片失效刷新重试'](https://blog.gintoki.cn/content/images/md_img/py_sublime%20text2.jpg)
#### 成功后重启Sublime Text
然后打开菜单 Sublime Text > Perferences > Package Control 看看是不点亮，若没有点亮请自行 google请参考其安装方法。

![alt='图片失效刷新重试'](https://blog.gintoki.cn/content/images/md_img/py_sublime%20text3.jpg)
###2. 添加SublimeREPL插件
####安装 SublimeREPL
打开菜单Sublime Text > Perferences > Package Control
输入Install Package回车
![alt='图片失效刷新重试'](https://blog.gintoki.cn/content/images/md_img/py_sublime%20text4.jpg)
输入SublimeREPL然后安装,安装成功后能看到菜单Tools里出现了 SublimeREPL。
####用SublimeREPL运行Python
菜单Tools > Python > Python - RUN current file
就能发现新打开了一个REPL控制台窗口，试试输入xxx发现能行。
![alt='图片失效刷新重试'](https://blog.gintoki.cn/content/images/md_img/py_sublime%20text5.jpg)
![alt='图片失效刷新重试'](https://blog.gintoki.cn/content/images/md_img/py_sublime%20text6.jpg)
####其他配置
#####多窗口显示
每次打开一个窗口并不方便调试查看，我希望在一个窗口中显示2个小窗口
，打开菜单 View > Layout > Columes:2，纵列现实2个窗口，若需要多个窗口可以自己选择。
![alt='图片失效刷新重试'](https://blog.gintoki.cn/content/images/md_img/py_sublime%20text7.jpg)
然后再运行一次就出现2个窗口，能够方便查看控制台输出结果了。
#####快捷键设置
每次运行Python都需要去菜单里点一次，很不方便，所以绑定一个快捷键能提高效率。</br>
Sublime Text > Perferences >Key Bindings-User </br>
在[ ]内添加下面内用，保存，我绑定到 F5，然后按快捷键试试。
		
	{"keys":["f5"],
	"caption": "SublimeREPL: Python - RUN current file",
	"command": "run_existing_window_command", "args":
	{
	"id": "repl_python_run",
	"file": "config/Python/Main.sublime-menu"
	}}
