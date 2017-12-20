#1.安装brew
#2.php
##安装
[https://github.com/Homebrew/homebrew-php](https://github.com/Homebrew/homebrew-php)

	brew tap homebrew/homebrew-php
	brew options php72
	
	he php.ini file can be found in:
    /usr/local/etc/php/7.2/php.ini

	✩✩✩✩ Extensions ✩✩✩✩
	
	If you are having issues with custom extension compiling, ensure that you are using the brew version, by placing /usr/local/bin before /usr/sbin in your PATH:
	
	      PATH="/usr/local/bin:$PATH"
	
	PHP72 Extensions will always be compiled against this PHP. Please install them using --without-homebrew-php to enable compiling against system PHP.
	
	✩✩✩✩ PHP CLI ✩✩✩✩
	
	If you wish to swap the PHP you use on the command line, you should add the following to ~/.bashrc, ~/.zshrc, ~/.profile or your shell's equivalent configuration file:
	  export PATH="$(brew --prefix homebrew/php/php72)/bin:$PATH"
	
	✩✩✩✩ FPM ✩✩✩✩
	
	To launch php-fpm on startup:
	    mkdir -p ~/Library/LaunchAgents
	    cp /usr/local/opt/php72/homebrew.mxcl.php72.plist ~/Library/LaunchAgents/
	    launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.php72.plist
	
	The control script is located at /usr/local/opt/php72/sbin/php72-fpm
	
	OS X 10.8 and newer come with php-fpm pre-installed, to ensure you are using the brew version you need to make sure /usr/local/sbin is before /usr/sbin in your PATH:
	
	  PATH="/usr/local/sbin:$PATH"
	
	You may also need to edit the plist to use the correct "UserName".
	
	Please note that the plist was called 'homebrew-php.josegonzalez.php72.plist' in old versions of this formula.
	
	With the release of macOS Sierra the Apache module is now not built by default. If you want to build it on your system you have to install php with the --with-httpd option. See  brew options php72 for more details.
	
	To have launchd start homebrew/php/php72 now and restart at login:
	  brew services start homebrew/php/php72
	==> Summary
	🍺  /usr/local/Cellar/php72/7.2.0_11: 350 files, 46.6MB
##配置路径
	/usr/local/etc/php/7.2/
##php-fpm

	/usr/local/sbin/php72-fpm start	
##启动重启
	禁用自带PHP
	pgrep php-fpm |xargs sudo kill -USR2
   
	sudo /usr/local/sbin/php72-fpm start
	sudo /usr/local/sbin/php72-fpm stop
	sudo /usr/local/sbin/php72-fpm restaret
##nginx
	#brew 搜索软件
	brew search nginx
	#brew 安装软件
	brew install nginx
	#brew 卸载软件
	brew uninstall nginx
	#brew 升级
	sudo brew update
	查看安装信息(经常用到, 比如查看安装目录等)
	sudo brew info nginx
	查看已经安装的软件
	brew list		
##nginx启动停止
	启动nginx服务
	sudo brew services start nginx
	查看nginx版本
	nginx -v
	关闭nginx服务
	sudo brew services stop nginx
	检查配置
	nginx -t
	热加载配置
	nginx -s reload
	停止nginx
	nginx -s stop
##nignx 配置
	配置目录/usr/local/etc/nginx/	

	
	
	