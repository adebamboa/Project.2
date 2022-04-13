## LEMP PROJECT

`sudo apt update` 


`sudo apt install nginx` 


`sudo systemctl status nginx` 



![NGINX-PNG](./images/NGINX-PNG.png)


`curl http://127.0.0.1:80` 


![CURL-PNG](./images/CURL-PNG.png)


`http://<Public-IP-Address>:80` 


`curl -s http://169.254.169.254/latest/meta-data/public-ipv4` 


![Welcome-NGINX-PNG](./images/Welcome-NGINX.png)


`sudo apt install mysql-server` 


`sudo mysql_secure_installation` 


`sudo mysql` 


![SQL-PNG](./images/SQL-PNG.png)


`mysql> exit` 

`sudo apt install php-fpm php-mysql` 


`sudo mkdir /var/www/projectLEMP` 



`sudo chown -R $USER:$USER /var/www/projectLEMP` 


`sudo nano /etc/nginx/sites-available/projectLEMP` 


`#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}`


`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`


`sudo nginx -t`


![NGINX-SYSTAX.PNG](./images/NGINX-SYSTAX.png)


`sudo unlink /etc/nginx/sites-enabled/default`

`sudo systemctl reload nginx`

`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

`http://<Public-IP-Address>:80`

![ECHO-MESSAGE.PNG](./images/ECHO-MESSAGE.png)

`sudo nano /var/www/projectLEMP/info.php`

`<?php
phpinfo();`

`http://`server_domain_or_IP`/info.php`


![PHP-IMAGE.PNG](./images/PHP-IMAGE.png)

`sudo rm /var/www/projectLEMP/info.php`

`sudo mysql`

`mysql> CREATE DATABASE `example_database`;`

`mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';`

`mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';`

`mysql> exit`

`mysql -u example_user -p`

`mysql> SHOW DATABASES;`

![SHOWDATABASE.PNG](./images/SHOW-DATABASE.png)

`CREATE TABLE example_database.todo_list (
mysql>     item_id INT AUTO_INCREMENT,
mysql>     content VARCHAR(255),
mysql>     PRIMARY KEY(item_id)
mysql> );`

`mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");`

`mysql>  SELECT * FROM example_database.todo_list;`

![EXAMPLE.PNG](./images/EXAMPLE.PNG)

`mysql> exit`

`nano /var/www/projectLEMP/todo_list.php`

`<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}`


`http://<Public_domain_or_IP>/todo_list.php`



![TODO.PNG](./images/TODO-IMAGE.png)







