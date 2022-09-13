# Project 2 - WEB STACK IMPLEMENTATION (LEMP STACK)

## Installing the Nginx Web Server


`sudo apt update`

`sudo apt update install nginx`


*Verifing that nginx was successfully installed*

`sudo systemctl status nginx`

Html image for ngix default page

`curl http://localhost:80`

![alt text](./Images/2%20-%20testing%20in%20browser.png/)


## **Installing MySQL**

`sudo apt install mysql-server`

`sudo mysql`

![alt text](./Images/3%20-%20connecting%20to%20mysql.png)


`sudo mysql_secure_installation`

![alt text](./Images/04%20-%20.png)


## **Installing PHP**

`sudo apt install php-fpm php-mysql`

`php -v`

![alt text](./Images/05%20-%20PHP%20Install.png)

## **Configuring Nginx to Use PHP Processor**

creating the web directory for domain

`sudo mkdir /var/www/projectLEMP`

`sudo chown -R $USER:$USER /var/www/projectLEMP`

`sudo nano /etc/nginx/sites-available/projectLEMP`

![alt text](./Images/06%20-%20writing%20into%20text%20editor.png)

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

`sudo nginx -t`

`sudo unlink /etc/nginx/sites-enabled/default`

`sudo systemctl reload nginx`

`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`


`http://3.82.99.231:80`


Testing on Browser
![alt text](./Images/08%20-%20testing%20on%20browser.png)


`sudo nano /var/www/projectLEMP/info.php`

*Testing PHP with ngix*

![alt text](./Images/09%20-.png)

`http://3.82.99.231/info.php`

![alt text](./Images/10%20-.png)


# **Retrieving data from MySQL database with PHP**

`sudo mysql`

`mysql> CREATE DATABASE `example_database`;`

`mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';`

`mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';`

`mysql> exit`

`mysql -u example_user -p`

`mysql> SHOW DATABASES;`

![alt text](./Images/11-%20loged%20in%20to%20user%20DB.png)


`mysql>CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT, content VARCHAR(255), PRIMARY KEY(item_id));`

`mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");`

`mysql> INSERT INTO example_database.todo_list (content) VALUES ("My second important item");`

`mysql> INSERT INTO example_database.todo_list (content) VALUES ("My third important item");`

`mysql> SELECT * FROM example_database.todo_list;`

`nano /var/www/projectLEMP/todo_list.php`

`<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";`


`try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();`
}


`http://3.82.99.231/todo_list.php`

![alt text](./Images/12.%20.png)