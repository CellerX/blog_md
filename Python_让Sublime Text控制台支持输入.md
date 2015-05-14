　昨天一直用iTerm运行Python ...我也是醉了，今天分别在sublime Text和Pycharm上体验了下。</br>
　Sublime Text编写python简单易用，适合我这种初学新手，但是遇到点棘手的地方，Sublime Text 运行带有 raw_input 的时候莫名其妙的报错，google了下发现Sublime Text Command+b 运行Python控制台不支持输入，于是继续google,找到一款插件[SublimeREPL](https://github.com/wuub/SublimeREPL)，安装方法:
　
###1. 为Sublime Text添加Installed Packages
若已经安装过略过
#### 使用Ctrl+`快捷键或者通过View->Show Console菜单打开命令行复制下面代码输入
	
	import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
#### 成功后重启Sublime Text
然后打开菜单 Sublime Text 》Perferences 》
	
###2. 添加SublimeREPL插件
#### 
