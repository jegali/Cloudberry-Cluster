# NGinx as reverse proxy
If individual servers such as a GIT, blog, WIKI and a CMS-managed web server based on Docker are running on the same or multiple host servers in a closed network, these services can be made externally accessible via a reverse proxy and then all accessed from the outside under port 80 and 443. A separate URL for each individual service then forwards the request to the correct server.

Of course, we will also look at an application example under Docker - but first, the website "mallowz" is to be hosted on one of the Raspberrys. The use case is as follows: A user in the internet types in http://aurorafox.de in his browser. The URL aurorafox.de is resolved by strato's DNS to my HP slice and will be served from the HP slice at 192.168.178.29. If the user types in http://aurorafox.de/mallowz in his browser, the URL is resolved by strato's DNS to my HP slice again, and then the NGinx will redirect /mallowz/ to the server http://192.168.178.101 which serves the mallowz website.

![win32diskimager](/images/reverse-proxy.png)


## Installing Nginx

Since Nginx is available in the default Ubuntu repositories, it can be installed from those repositories using the apt package system. We install NGinx by typing these commands:

```bash
sudo apt update
sudo apt install nginx
```

At the end of the installation process, Ubuntu 21 starts Nginx. The web server should already be running. You can perform a check with the systemd init system to ensure that the service is running by entering the following:

```bash
systemctl status nginx
```

Now that your web server is running, let's take a look at some basic administrative commands. To stop your web server, type the following:

```bash
sudo systemctl stop nginx
```

To start the web server when it has been stopped, type the following:

```bash
sudo systemctl start nginx
```

To stop and restart the service, type the following:

```bash
sudo systemctl restart nginx
```

If you are only making configuration changes, Nginx can often reload without dropping connections. To do this, type the following:

```bash
sudo systemctl reload nginx
```

By default, Nginx is configured to start automatically when the server boots. If you do not want this behavior, you can disable it by typing the following:

```bash
sudo systemctl disable nginx
```

Enter the following to re-enable the service to start at boot time:

```bash
sudo systemctl enable nginx
```

You have now learned basic management commands and can begin to configure the site to host more than one domain.
