#Ubuntu 16.04♥中的TYPO3

由于大部分操作都需要使用root权限，默认都以root用户操作

	sudo su

###Nginx

下载Key文件

	wget http://nginx.org/keys/nginx_signing.key

安装Key文件

	apt-key add nginx_signing.key

修改`/etc/apt/sources.list`文件，并在文件末尾增加

	deb http://nginx.org/packages/ubuntu/ xenial nginx
	deb-src http://nginx.org/packages/ubuntu/ xenial nginx

更新APT源并安装Nginx

	apt-get update
	apt-get install nginx

实际步骤以[官方安装文档](http://nginx.org/en/linux_packages.html)为准

###MySQL

	apt-get install mysql-server

###PHP7

安装PHP7-FPM及相关插件

	apt-get install php7.0-curl php7.0-fpm php7.0-gd php7.0-mbstring php7.0-mcrypt php7.0-mysql php7.0-soap php7.0-xml php7.0-zip

###站点配置

**以下内容仅作为参考**

创建`/var/www/domain.site/httpdocs/`

	mkdir -p /var/www/domain.site/httpdocs

设置用户和用户组

	chown -R www-data:www-data /var/www/domain.site/httpdocs

编辑`/etc/nginx/fastcgi_params`，添加

	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;


新建站点配置文件`/etc/nginx/conf.d/domain.site.conf`

	server {
		listen 80;
		server_name domain.site;
		access_log /var/www/domain.site/access.log main;
		error_log /var/www/domain.site/error.log warn;
		root /var/www/domain.site/httpdocs/;
		index index.html index.htm index.php;
		location ~ \.php$ {
			fastcgi_pass unix:/run/php/php7.0-fpm.sock;
			include fastcgi_params;
		}
	}

重启Nginx

	service nginx restart

编辑`/etc/php/7.0/fpm/php.ini`

	max_execution_time=240
	max_input_vars=1500

编辑`/etc/php/7.0/fpm/pool.d/www.conf`

	listen_owner = nginx
	listen_group = nginx

重启PHP7-FPM

	service php7.0-fpm restart

# TYPO3

从[TYPO3官网](https://typo3.org/download/)下载最新版本至`/var/www/`并解压

	cd /var/www/
	wget http://prdownloads.sourceforge.net/typo3/typo3_src-7.6.9.tar.gz
	tar xzf typo3/typo3_src-7.6.9.tar.gz

安装前的准备工作

	cd /var/www/domain.site/httpdocs
	ln -fs /var/www/typo3_src-7.6.9 typo3_src
	ln -fs typo3_src/index.php
	ln -fs typo3_src/typo3
	chown -R www-data:www-data *
	touch FIRST_INSTALL

创建新MySQL相关记录

	mysql -uroot -p
	CREATE USER typo3 IDENTIFIED BY 'password';
	CREATE DATABASE domain;
	GRANT ALL ON domain.* TO 'typo3';

浏览器访问`http://domain.site`进行安装TYPO3