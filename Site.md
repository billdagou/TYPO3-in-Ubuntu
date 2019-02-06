# Ubuntu 18.04♥中的TYPO3 —— 站点配置

**以下内容仅作为参考**

创建站点根目录`/var/www/domain.site/httpdocs/`

	mkdir -p /var/www/domain.site/httpdocs

设置用户和用户组

	chown -R www-data:www-data /var/www/domain.site/httpdocs

新建配置文件`/etc/php/7.2/fpm/pool.d/zzz.conf`（加载顺序需在`www.conf`之后）

	[www]
	listen.owner = nginx
	listen.group = nginx

重启PHP-FPM

	service php7.2-fpm restart

编辑`/etc/nginx/fastcgi_params`，添加

	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
	fastcgi_pass unix:/run/php/php7.2-fpm.sock;

新建站点配置文件`/etc/nginx/conf.d/domain.site.conf`

	server {
		listen 80;
		server_name domain.site;
		access_log /var/www/domain.site/access.log main;
		error_log /var/www/domain.site/error.log warn;
		root /var/www/domain.site/httpdocs/;
		index index.html index.htm index.php;
		location ~ \.php$ {
			include fastcgi_params;
		}
	}

重启Nginx

	service nginx restart

[>> TYPO3](TYPO3.md)