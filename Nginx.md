# Ubuntu 16.04♥中的TYPO3 —— Nginx

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

*实际步骤以[官方安装文档](http://nginx.org/en/linux_packages.html)为准*

[>> MySQL](./MySQL.md)