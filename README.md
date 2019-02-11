# Ubuntu 18.04♥中的TYPO3

由于大部分操作都需要使用root权限，默认都以root用户操作

	sudo su

在开始前，先更新并升级系统

    apt update
    apt upgrade

1. [Nginx](Nginx.md)
2. [MySQL](MySQL.md)
3. [PHP](PHP.md)
4. [站点配置](Site.md)
5. [TYPO3](TYPO3.md)

可选配置
* Nginx
    * [站点重定向](Redirect.md)
    * [Mime Types](MimeTypes.md)
    * [页面压缩](GZip.md)
    * [资源缓存](Expires.md)
    * [HTTPS](Https.md)
* PHP
    * [文件上传](Upload.md)
* 站点
    * [站点配置（完整）](SiteConfiguration.md)
* TYPO3
    * [应用上下文](ApplicationContext.md)
    * [访问权限](Access.md)
    * [Grunt](Grunt.md)