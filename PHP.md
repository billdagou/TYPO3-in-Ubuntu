# Ubuntu 18.04♥中的TYPO3 —— PHP

**Ubuntu 18.04默认使用PHP7.2**

激活`universe`（默认只有`main`），并更新

    add-apt-repository universe
    apt update

安装PHP-FPM及相关插件

    apt install php7.2-curl php7.2-fpm php7.2-gd php7.2-intl php7.2-mbstring php7.2-mysql php7.2-xml php7.2-zip

重启PHP-FPM服务

	service php7.2-fpm restart

如果有额外插件的需求，请自行安装。

[>> 站点配置](Site.md)