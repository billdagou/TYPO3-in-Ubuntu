# Ubuntu 22.04♥中的TYPO3 —— Nginx

安装依赖

    apt install curl gnupg2 ca-certificates lsb-release ubuntu-keyring

下载Key文件

    curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
        | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null

创建稳定版的APT源

    echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
    http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
        | sudo tee /etc/apt/sources.list.d/nginx.list

设置优先级

    echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
        | sudo tee /etc/apt/preferences.d/99nginx

安装Nginx

    apt update
    apt install nginx

*实际步骤以[官方安装文档](http://nginx.org/en/linux_packages.html#Ubuntu)为准*

[>> MySQL](MySQL.md)