# Ubuntu 22.04♥中的TYPO3 —— PHP

**Ubuntu 22.04默认使用PHP8.1**

安装PHP-FPM及相关插件

    apt install php8.1-curl php8.1-fpm php8.1-gd php8.1-intl php8.1-mbstring php8.1-mysql php8.1-xml php8.1-zip

重启PHP-FPM服务

    service php8.1-fpm restart

如果有额外插件的需求，请自行安装。

[>> 站点配置](Site.md)