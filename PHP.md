# Ubuntu 24.04♥中的TYPO3 —— PHP

**Ubuntu 24.04默认使用PHP8.3**

安装PHP-FPM及相关插件

    apt install php8.3-curl php8.3-fpm php8.3-gd php8.3-intl php8.3-mbstring php8.3-mysql php8.3-xml php8.3-zip

重启PHP-FPM服务

    service php8.3-fpm restart

如果有额外插件的需求，请自行安装。

[>> 站点配置](Site.md)