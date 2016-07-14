#Ubuntu 16.04♥中的TYPO3 —— 站点配置

**以下内容仅作为参考**

创建`/var/www/domain.site/httpdocs/`

	mkdir -p /var/www/domain.site/httpdocs

设置用户和用户组

	chown -R www-data:www-data /var/www/domain.site/httpdocs

编辑`/etc/php/7.0/fpm/pool.d/www.conf`

	listen_owner = nginx
	listen_group = nginx

重启PHP-FPM

	service php7.0-fpm restart

编辑`/etc/nginx/fastcgi_params`，添加

	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

新建站点配置文件`/etc/nginx/conf.d/domain.site.conf`

	server {
		listen 80;
		server_name domain.site;
		access_log /var/www/domain.site/access.log main;
		error_log /var/www/domain.site/error.log warn;
		root /var/www/domain.site/httpdocs/;
		index index.html index.htm index.php;
		location ~ \.php$ {
			fastcgi_pass unix:/run/php/php7.0-fpm.sock;
			include fastcgi_params;
		}
	}

重启Nginx

	service nginx restart

如需采用TCP socket（默认为Unix socket）方式连接，修改`/etc/php/7.0/fpm/pool.d/www.conf`

	listen = 127.0.0.1:9000

站点配置文件`/etc/nginx/conf.d/domain.site.conf`

	fastcgi_pass 127.0.0.1:9000;

重启相应服务

	service php7.0-fpm restart
	service nginx restart

[>> TYPO3](./TYPO3.md)