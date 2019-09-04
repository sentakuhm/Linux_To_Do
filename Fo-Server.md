#############Installing Nginx, MySQL, PHP (LEMP) Stack##########
0/ `$sudo ufw enable`
1/ `$sudo apt install nginx`
2/ `$sudo ufw allow OpenSSH`
3/ `$sudo ufw allow 'Nginx HTTP'`
4/ check with: `$sudo ufw status`
5/ check ip in browser
#######Install MySQL###########
1/ `$sudo apt install mysql-server`
2/ `$sudo mysql_secure_installation`
then edit:
n
y
y
y
y
3/ then check with: `$sudo mysqladmin -p -u root version`
########Install PHP############
1/ sudo apt install php-fpm php-mysql
2/ edit /etc/nginx/sites-available/default
add: index.php like
	index index.php index.html index.htm index.nginx-debian.html;
change server_name YOUR_DOMAIN_OR_IP_HERE;
and change and uncomment like:
	location ~ \.php$ {
                include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        }
3/ restart Nginx: `$sudo nginx -t`
		  `$sudo service nginx reload`
4/ test with: `$sudo nano /var/www/html/info.php and add`
	```<?php
        phpinfo();
        ?>```
then remove it
`$sudo rm /var/www/html/info.php`
5/ install phpmyadmin
then run: `$sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin`

###########IP Config###################
backup default first: `$sudo cp /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.bak`
`$sudo vim /etc/netplan/50-cloud-init.yaml`
```network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: yes
    enp0s8:
      dhcp4: no
      dhcp6: no
      addresses: [192.168.56.91/24, ]
      gateway4: 192.168.56.1
      nameservers:
        addresses: [1.1.1.1,1.0.0.1]```
	
##########Mysql Conf################
Login to MySQL by run:
`$sudo mysql -p -u root`
`$CREATE USER 'admin'@'%' IDENTIFIED BY 'add your passwd';` 
`$GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;`