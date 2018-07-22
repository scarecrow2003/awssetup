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

  wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
  sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm
  sudo yum install -y mysql-server
  sudo rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
  sudo yum install -y vim httpd nginx wget unzip php php-mysql php-gd php-pear mod_ssl
  sudo chkconfig httpd on
  sudo chkconfig nginx on
  sudo chkconfig mysqld on
  
3. Assign the Elastic IP to the above instance

Server setup
1. Secure mysql
  sudo grep 'temporary password' /var/log/mysqld.log
  sudo mysql_secure_installation
2. Config httpd, nginx, mysql
5. Copy uploads fold (S3)
6. Copy html folder and mysqldump
7. Import mysqldump
8. Install gcc, ImageMagick
9. Change ssh port
10. Install Denyhosts


Install Postfix https://seasonofcode.com/posts/custom-domain-e-mails-with-postfix-and-gmail-the-missing-tutorial.html
