# Ubuntu 18.04♥中的TYPO3 —— Nginx

下载Key文件

	wget https://nginx.org/keys/nginx_signing.key

安装Key文件

	apt-key add nginx_signing.key

新增APT源`/etc/apt/sources.list.d/nginx.list`

	deb http://nginx.org/packages/ubuntu bionic nginx

安装Nginx

	apt update
	apt install nginx

*实际步骤以[官方安装文档](http://nginx.org/en/linux_packages.html#Ubuntu)为准*

[>> MySQL](MySQL.md)