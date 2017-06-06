# Ubuntu 16.04♥中的TYPO3 —— PHP

**Ubuntu 16.04默认使用PHP7**

APT安装PHP-FPM及相关插件

	apt-get install php-apcu php7.0-curl php7.0-fpm php7.0-gd php7.0-mbstring php7.0-mcrypt php7.0-mysql php7.0-soap php7.0-xml php7.0-zip

启用APCu插件

	phpenmod apcu

编辑`/etc/php/7.0/mods-available/apcu.ini`，开启APCu的Cli支持。如有需要，使用`apc.shm_size`修改APCu的内存使用空间。

	apc.enable_cli=On
	#apc.shm_size=128M

重启PHP-FPM服务

	service php7.0-fpm restart

如果有额外插件的需求，请自行安装。

[>> 站点配置](./Site.md)