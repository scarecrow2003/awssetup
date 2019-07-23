# awssetup
IAM
1. Create one group with AmazonRDSFullAccess, AMazonEC2FullAccess, AmazonElastiCacheFullAccess, AmazonS3FullAccess and AdministratorAccess
2. Create one user attached to the above group

VPC
1. Change to Singapore
2. Create security group with inbound ports 80, 22(60914), 25(465), 11211, 443, 587
3. Create Elastic IPs

EC2
1. Create key pair and download
2. Create instance

  ```wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm```
  ```sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm```
  ```sudo yum install -y mysql-server```
  ```sudo rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm```
  ```sudo yum install -y vim httpd wget unzip php php-mysql php-gd php-pear mod_ssl```
  ```sudo chkconfig httpd on```
  ```sudo chkconfig nginx on```
  ```sudo chkconfig mysqld on```
  
3. Assign the Elastic IP to the above instance

Server setup
1. Secure mysql
  `systemctl mysqld start`
  `sudo mysql_secure_installation`
2. Config httpd, nginx, mysql, .htaccess
  `httpd.conf`:
  ```Listen 8008```
  `vhost.conf`:
  ```NameVirtualHost 127.0.0.1:8008
  <VirtualHost 127.0.0.1:8008>
    ServerAdmin contactus@appletreesg.com
    DocumentRoot /var/www/html
    ServerName www.appletreesg.com
    <Directory "/var/www/html">
      RewriteEngine On
      RewriteBase /
      RewriteRule ^index\.php$ - [L]
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteCond %{REQUEST_FILENAME} !-d
      RewriteRule . /index.php [L]
    </Directory>
    ErrorLog /var/log/httpd/error_log
    CustomLog /var/log/httpd/access_log common
</VirtualHost>```
`default.conf`:
```server {
    listen       80;
    server_name  appletreesg.com ;
    return       301 http://www.appletreesg.com$request_uri;
}

server {
    listen       80 default_server;
    server_name  www.appletreesg.com;
    return      301 https://$server_name$request_uri;
}

server {
   listen 443;
   ssl on;
   ssl_certificate /etc/nginx/ssl/appletreesg-cloudflare.pem;
   ssl_certificate_key /etc/nginx/ssl/appletreesg-cloudflare.key;

   ssl_protocols TLSv1.2;
   server_name www.appletreeesg.com;
   access_log /var/log/nginx/ats-ssl.access.log;
   error_log /var/log/nginx/ats-ssl.error.log;

   location / {
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_pass http://127.0.0.1:8008;
    }
}```
`proxy_params`:
```proxy_set_header Host $http_host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Host $host;
proxy_set_header X-Forwarded-Proto $scheme;```
`appletreesg-cloudflare.key` `appletreesg-cloudflare.pem`
5. Copy uploads fold (S3)
6. Copy html folder and mysqldump
7. Import mysqldump
8. Install gcc, ImageMagick
9. Change ssh port
10. Install Denyhosts


Install Postfix https://seasonofcode.com/posts/custom-domain-e-mails-with-postfix-and-gmail-the-missing-tutorial.html
