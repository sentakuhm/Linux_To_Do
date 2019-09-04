#############Installing Nginx, MySQL, PHP (LEMP) Stack##########<br>
0/ `$sudo ufw enable`<br>
1/ `$sudo apt install nginx`<br>
2/ `$sudo ufw allow OpenSSH`<br>
3/ `$sudo ufw allow 'Nginx HTTP'`<br>
4/ check with: `$sudo ufw status`<br>
5/ check ip in browser<br>
#######Install MySQL###########<br>
1/ `$sudo apt install mysql-server`<br>
2/ `$sudo mysql_secure_installation`<br>
then edit:<br>
n<br>
y<br>
y<br>
y<br>
y<br>
3/ then check with: `$sudo mysqladmin -p -u root version`<br>
########Install PHP############<br>
1/ sudo apt install php-fpm php-mysql<br>
2/ edit /etc/nginx/sites-available/default<br>
add: index.php like<br>
	index index.php index.html index.htm index.nginx-debian.html;<br>
change server_name YOUR_DOMAIN_OR_IP_HERE;<br>
and change and uncomment like:<br>
	location ~ \.php$ {<br>
                include snippets/fastcgi-php.conf;<br>
        #<br>
        #       # With php-fpm (or other unix sockets):<br>
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;<br>
        #       # With php-cgi (or other tcp sockets):<br>
        #       fastcgi_pass 127.0.0.1:9000;<br>
        }<br>
3/ restart Nginx: `$sudo nginx -t`<br>
		  `$sudo service nginx reload`<br>
4/ test with: `$sudo nano /var/www/html/info.php and add`<br>
	```<?php
        phpinfo();
        ?>```
then remove it<br>
`$sudo rm /var/www/html/info.php`<br>
5/ install phpmyadmin<br>
then run: `$sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin`<br>

###########IP Config###################<br>
backup default first: `$sudo cp /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.bak`<br>
`$sudo vim /etc/netplan/50-cloud-init.yaml`<br>
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
	
##########Mysql Conf################<br>
Login to MySQL by run:<br>
`$sudo mysql -p -u root`<br>
`$CREATE USER 'admin'@'%' IDENTIFIED BY 'add your passwd';`<br> 
`$GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;`
