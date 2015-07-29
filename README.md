# nginx php-fpm 运行环境搭建。

CentOS/Ubuntu 系统的 nginx php-fpm 运行环境搭建。
全文以yum/apt-get部署，以便升级。
有用到中国境内yum源，感谢这些企业对开源社区的支持。

献给我组3位可爱的新同学。

# 目录
-----
1. [准备工作](#准备工作)
   * [CentOS](#init-centos)
   * [Ubuntu](#init-ubuntu)
2. [配置环境](#configuring)
   * [CentOS](#config-centos)
   * [ubuntu](#config-ubuntu)

-----

# 准备工作
-----

## CentOS
1. 安装epel & nginx 官网yum源 & remi php-fpm源
-----
CentOS7
~~~
rpm -ivh http://mirrors.opencas.cn/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
rpm -ivh http://nginx.org/packages/rhel/7/noarch/RPMS/nginx-release-rhel-7-0.el7.ngx.noarch.rpm
rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
~~~
CentOS6
~~~
rpm -ivh http://mirrors.sohu.com/fedora-epel/6/i386/epel-release-6-8.noarch.rpm
rpm -ivh http://nginx.org/packages/rhel/6/noarch/RPMS/nginx-release-rhel-6-0.el6.ngx.noarch.rpm
rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
~~~
CentOS5
~~~
rpm -ivh http://mirrors.opencas.cn/epel/5/i386/epel-release-5-4.noarch.rpm
rpm -ivh http://nginx.org/packages/rhel/5/noarch/RPMS/nginx-release-rhel-5-0.el5.ngx.noarch.rpm
rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-5.rpm
~~~


## nginx php-fpm 监控
~~~
location /status {
    #auth_basic "Password please";
    #auth_basic_user_file http_auth;
    allow 127.0.0.1;    

    stub_status on; 
    access_log   off;
      }   

location ~ ^/(php_status|php_ping)$ {
#location /php_status {
    include fastcgi_params;
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_param SCRIPT_FILENAME $fastcgi_script_name;

    access_log   off;
}   
~~~
