# webserver

```
###### Prerequisites
- Centos 7.x
- require root access

###### which will be installed
- php 
- httpd 
- mariadb 
- ffmpeg

###### update all installed packages
yum update
```

## Install PHP
###### install repository and config-manager
```
###### install repository
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm

###### Install config manager
yum install yum-utils
```
###### Enable config-manager and installing php 5.6 
```
yum-config-manager --enable remi-php56

###### Install php 5.6
yum install php php-mysql php-mcrypt php-xml php-simplexml php-mbstring php-fpm -y

###### check version
php -v
```

## Install webserver
```
###### installing webserver
yum install httpd 
systemctl start httpd 

###### check version
httpd -v

###### check status 
systemctl status httpd

###### create virtualHost
chown -R apache:apache /var/www/html/
chmod -R 775 /var/www/

cat > /etc/httpd/conf.d/site.conf <<EOF
<VirtualHost *:80>
    ServerName yourdomain.com
    # ServerAlias yourdomain.com
    DocumentRoot /var/www/html
    #ErrorLog /var/www/html/error_logs/error.log
    #CustomLog /var/www/html/error_logs/requests.log combined
</VirtualHost>
EOF

###### restart service
systemctl restart httpd
```

## Install and setting Database
```
###### installing mariadb 
yum install mariadb-server mariadb
systemctl start mariadb

###### setting passwd 
mysql_secure_installation

###### check mysql status
systemctl status mariadb

###### check mysql version
mysql -V

###### test login
mysql -u root -p
```

## Install ffmpeg
###### Import the repository GPG key and enable Nux reository
```
###### Installing NUX repository 
rpm -v --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm 

###### install FFmpeg
yum install ffmpeg ffmpeg-devel

###### check version
ffmpeg -version
```
