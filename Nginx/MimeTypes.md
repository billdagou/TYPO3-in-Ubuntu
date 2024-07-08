# Ubuntu 24.04♥中的TYPO3 —— Mime Types

新建Mime Type配置文件`/etc/nginx/conf.d/mime.types.conf`

    types {
        # Data interchange
        application/atom+xml                        atom;
        application/json                            json map topojson;
        application/ld+json                         jsonld;
        application/rss+xml                         rss;
        application/vnd.geo+json                    geojson;
        application/xml                             rdf xml;

        # JavaScript
        application/javascript                      js;

        # Manifest files
        application/manifest+json                   webmanifest;
        application/x-web-app-manifest+json         webapp;
        text/cache-manifest                         appcache;

        # Media files
        audio/mp4                                   f4a f4b m4a;
        audio/ogg                                   oga ogg opus;
        image/bmp                                   bmp;
        image/svg+xml                               svg svgz;
        image/webp                                  webp;
        video/mp4                                   f4v f4p m4v mp4;
        video/ogg                                   ogv;
        video/webm                                  webm;
        video/x-flv                                 flv;
        image/x-icon                                cur ico;

        # Web fonts
        application/font-woff                       woff;
        application/font-woff2                      woff2;
        application/vnd.ms-fontobject               eot
        application/x-font-ttf                      ttc ttf;
        font/opentype                               otf;

        # Other
        application/octet-stream                    safariextz;
        application/x-bb-appworld                   bbaw;
        application/x-chrome-extension              crx;
        application/x-opera-extension               oex;
        application/x-xpinstall                     xpi;
        text/vcard                                  vcard vcf;
        text/vnd.rim.location.xloc                  xloc;
        text/vtt                                    vtt;
        text/x-component                            htc;
    }

重启Nginx

    service nginx restart

*详细配置以[官方文档](http://nginx.org/en/docs/http/ngx_http_core_module.html#types)为准*

[<< 返回](../README.md)