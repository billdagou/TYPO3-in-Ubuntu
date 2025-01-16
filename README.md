# Ubuntu 24.04♥中的TYPO3

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
* MySQL
    * [Binlog](MySQL/Binlog.md) 
* Nginx
    * [资源缓存](Nginx/Expires.md)
    * [页面压缩](Nginx/GZip.md)
    * [HTTPS](Nginx/Https.md)
    * [Mime Types](Nginx/MimeTypes.md)
    * [站点重定向](Nginx/Redirect.md)
* PHP
    * [文件上传](PHP/Upload.md)
* 站点
    * [站点配置（完整）](Site/Configuration.md)
* TYPO3
    * [访问权限](TYPO3/Access.md)
    * [应用上下文](TYPO3/ApplicationContext.md)
    * [Grunt](TYPO3/Grunt.md)
    * [资源压缩](TYPO3/GZip.md)
    * [版本文件](TYPO3/Version.md)