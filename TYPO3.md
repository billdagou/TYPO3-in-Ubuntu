#Ubuntu 16.04♥中的TYPO3 —— TYPO3

编辑`/etc/php/7.0/fpm/php.ini`

	max_execution_time=240
	max_input_vars=1500

安装ImageMagick/GraphicsMagick，推荐GraphicsMagick

	apt-get install graphicsmagick

从[TYPO3官网](https://typo3.org/download/)下载最新版本（假设为v7.6.9）至`/var/www/`并解压

	cd /var/www/
	wget https://get.typo3.org/7.6.9
	tar xzf typo3_src-7.6.9.tar.gz

安装前的准备工作

	cd /var/www/domain.site/httpdocs
	ln -fs /var/www/typo3_src-7.6.9 typo3_src
	ln -fs typo3_src/index.php
	ln -fs typo3_src/typo3
	chown -R www-data:www-data *
	touch FIRST_INSTALL

创建数据库相关记录

	mysql -uroot -p
	CREATE USER typo3 IDENTIFIED BY 'password';
	CREATE DATABASE domain DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
	GRANT ALL ON domain.* TO 'typo3';

浏览器访问`http://domain.site`进行后续安装。

[>> 返回](./README.md)