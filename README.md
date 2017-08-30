# awssetup
IAM
1. Create one group with AmazonRDSFullAccess, AMazonEC2FullAccess, AmazonElastiCacheFullAccess, AmazonS3FullAccess and AdministratorAccess
2. Create one user attached to the above group

VPC
1. Create security group with inbound ports 80, 22(60914), 25(465), 11211, 443, 587
2. Create Elastic IPs

EC2
1. Create key pair and download
2. Create instance
3. Assign the Elastic IP to the above instance

Server setup
1. Install httpd, nginx, wget, unzip, mysql, php, php-mysql, php-gd, php-pear
2. Enable auto start for httpd, nginx, mysql
3. Install vim
4. Config nginx, httpd
5. Copy uploads fold (S3)
6. Copy html folder and mysqldump
7. Import mysqldump
8. Install gcc, ImageMagick
9. Change ssh port
10. Install Postfix https://seasonofcode.com/posts/custom-domain-e-mails-with-postfix-and-gmail-the-missing-tutorial.html
11. Install Denyhosts
