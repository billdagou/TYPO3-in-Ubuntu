# Ubuntu 20.04♥中的TYPO3 —— PHP

**Ubuntu 20.04默认使用PHP7.4**

安装PHP-FPM及相关插件

    apt install php7.4-curl php7.4-fpm php7.4-gd php7.4-intl php7.4-mbstring php7.4-mysql php7.4-xml php7.4-zip

重启PHP-FPM服务

    service php7.4-fpm restart

如果有额外插件的需求，请自行安装。

[>> 站点配置](Site.md)