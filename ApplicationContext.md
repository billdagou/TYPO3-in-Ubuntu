# Ubuntu 20.04♥中的TYPO3 —— 应用上下文

修改站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        ...
        location ~ \.php$ {
            fastcgi_param TYPO3_CONTEXT value;
        }
    }

可选值为`Production`、`Development`、`Testing`，更多详情请参考`\TYPO3\CMS\Core\Core\ApplicationContext`。

重启Nginx

    service nginx restart

[<< 返回](README.md)