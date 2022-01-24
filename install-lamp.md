# Install LAMP on a Raspberry with IP 192.168.178.101
With a LAMP server (Linux Apache MySQL PHP), any Linux computer can be turned into a functioning web server. Especially the current Raspberry Pi 4 is perfectly suited for use as a compact web server thanks to its fast network interfaces: In this document we set up the webshop "mallowz" as a hackable LAMP installation.

```bash
sudo apt-get install apache2 libapache2-mod-php php php-mysql mariadb-server mariadb-client
```

That's basically it: You can now test the Raspberry web server by simply accessing the default Apache web server page on your browser. Just type http://192.168.178.101 into your browser. You should now see the default Apache server website.

The website is located in the folder /var/www/html/. You now can use any editor of your choice to edit the page or upload your own websote via filezilla or another ftp-tool. Next you can test the PHP function: Create a file named "index.php" in the folder /var/www/html/ on the Raspberry. You can rename the existing index.html to something like "index.old". Then you write some PHP command like 
  
```bash
<?php echo "Hello world! This is the best website of the world"; ?>
```
  
into the index.php file, save it and reload http://192.168.178.101. If "Hello world! ..." is output? Perfect: You can use your web server now. To view the PHP information you can also use

```bash
<?php phpinfo(); ?>
```

in the file.

# Install phpMyAdmin on the Raspberry
phpMyAdmin is a free software tool written in PHP, intended to handle the administration of MySQL using a web interface.

To install phpMyAdmin on a Raspberry Pi, type the following command into the terminal:

```bash
sudo apt install phpmyadmin -y
```

The phpMyAdmin installation program will ask you few questions. We’ll use the dbconfig-common.

*Select Apache2 when prompted and press the Enter key
*Configuring phpmyadmin? OK
*Configure database for phpmyadmin with dbconfig-common? Yes
*Type your password and press OK
