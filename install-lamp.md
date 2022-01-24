# Install LAMP on a Raspberry
With a LAMP server (Linux Apache MySQL PHP), any Linux computer can be turned into a functioning web server. Especially the current Raspberry Pi 4 is perfectly suited for use as a compact web server thanks to its fast network interfaces: In this document we set up the webshop "mallowz" as a hackable LAMP installation.

```bash
sudo apt-get install apache2 libapache2-mod-php php php-mysql mariadb-server mariadb-client
```

That's basically it: You can now test the Raspberry web server by simply accessing the default Apache web server page on your browser. Just type http://<ip-address> into your browser. You should now see the default Apache server website.
