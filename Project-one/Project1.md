# **LAMP STACK IMPLEMENTATION (LAMP STACK) IN AWS**

*Login to EC2 Server*

![alt text](./Images/Log%20in%20to%20EC2%20Server.png)



`sudo apt update`

`sudo apt install apache2`

`sudo systemctl status apache2`

---

![alt text](./Images/2.%20Verifying%20Apache%20installed.png)


## Html Image for apache2 default page


![alt text](./Images/3.%20Testing%20Apache%20in%20the%20browser.png)




## **My SQL Installation**

`sudo apt install mysql-server`

`sudo mysql`

![alt text](./Images/4.%20Install%20mysql.png)

`sudo mysql_secure_installation`

![alt text](./Images/5%20-%20Testing%20mysql.png)


## PHP Installation

`sudo apt install php libapache2-mod-php php-mysql`

php -v

![alt text](./Images/6-%20Php%20Installation.png)

## Creating Virtual Host using Apache

`sudo mkdir /var/www/projectlamp`

`sudo chown -R $USER:$USER /var/www/projectlamp`

`sudo vi /etc/apache2/sites-available/projectlamp.conf`

![alt text](./Images/7-.png)


`sudo ls /etc/apache2/sites-available`

`sudo a2ensite projectlamp`

`sudo a2dissite 000-default`

`sudo apache2ctl configtest`

`sudo systemctl reload apache2`

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`



**Checking the status code on web browser**

![alt text](./Images/8-.png)


## Enabling PHP on Website

`sudo vim /etc/apache2/mods-enabled/dir.conf`

`{
<IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
}`

`sudo systemctl reload apache2`

`vim /var/www/projectlamp/index.php`

![alt text](./Images/9-.png)


*checking code status on browser*

![alt text](./Images/10%20-.png)


