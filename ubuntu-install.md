# Raspberry Installation
As already told in the [architectural section](https://github.com/jegali/Cloudberry-Cluster/blob/main/architecture.md), the Raspberry will also be equipped with Ubuntu 21. I decided to install only one node completely. I know that an external monitor (and a mouse and keyboard) will be needed at the beginning of the configuration, so I only want to do this installation process once to avoid having to constantly replug everything. Then openSSH and RDP will be installed to do the rest remotely. <br/>


I equipped each Raspberry with a 128GB SD card to be ready for the future. However, the disadvantage of a card of this size is also obvious - if the card is to be cloned, it just takes a little longer. In my case, it took about 1 hour to read the card, and then about 40 minutes to flash each additional instance. With eight cards, it can take a day.
By and large, I followed this website for the basic installation:

![Ubuntu Install](/images/ubuntu-1.png)

https://ubuntu.com/tutorials/how-to-install-ubuntu-desktop-on-raspberry-pi-4#1-overview

The website does a good job, including introducing Raspberry's imaging tool, which should definitely be used. The trick with the SSH file unfortunately did not work for me, but it may also be that this approach does not work under ubuntu in general, since the OpenSSH server still needs to be post-installed.

The guided installation should be carried out in any case to the end - because here you can directly assign a user account and password, make country-specific settings, give the computer a name and update the system to the latest version. Of course, you can also do this 8 times in a row or quasi-parallel - but since you need a screen and a keyboard, you would have to reconnect all the time. This way, an installation can be performed and then the SD card can be cloned.

For cloning I recommend the software Win32 Disk Imager, which can be downloaded and installed at the link below. In principle, this works exactly like the Pi Imager, but can also create images.

![win32diskimager](/images/win32diskimager.png)

https://sourceforge.net/projects/win32diskimager/

The operation of the software is very intuitive, so I'll skip a tutorial at this point. But before the SD card can be cloned, some software should be installed so that the individual Raspberry can be controlled headless after the cloning process - i.e. without using an external keyboard, monitor and mouse. 

## Installing additional software
After installing and configuring the basic system, I installed an OpenSSH server so that I can continue the rest of the installation steps from my PC. On the freshly installed system, open a console and install SSH through

```bash
sudo apt-get install openssh-server
```

You will be asked for the password of the user you created in the installation process. The installation routine has automatically added this to the Sudoer group. This can be convenient, but it can also be a security risk. Decide for yourself whether you want to keep your user in this group. A system boot should not be necessary after installation, so you can connect directly to the Raspberry via ssh or Putty or any other software of your choice. After successfully logging in to the ubuntu system, you can now bring it up to date. Use these commands to do this:

```bash
sudo apt-get update
sudo apt-get upgrade
```

Personally, I get along well with ssh as a command line, but sometimes it still makes sense to administrate via a graphical interface. To be able to do this, I have additionally installed xrdp on the Raspberry. To do this, execute these commands in the console:

```bash
sudo apt install xrdp
sudo adduser xrdp ssl-cert
sudo systemctl restart xrdp
sudo ufw allow 3389
sudo apt install xfce4
```

Now you have to edit the file /etc/xrdp/startwm.sh to change the desktop system from gnome to xfce4 which is absolutely sufficient and more performant through RDP sessions.

```bash
sudo nano /etc/xrdp/startwm.sh
```

Find these lines and comment them out with a "#"

```bash
test -x /etc/X11/Xsession && exec /etc/X11/Xsession 
exec /bin/sh /etc/X11/Xsession 
```

then add

```bash
startxfce
```

instead. Save the file, exit nano and restart the system by typing the command

```bash
sudo reboot now
```

If you are using windows, start you Remote Desktop Protocol and connect to your machine's IP. The user is the user you created during the installation process. The terminal may not start when you select it from the menu. This is usually because gnome-terminal is still entered as the default terminal. But this is not a big problem. Connect again via ssh and enter 

```bash
sudo update-alternatives –config x-terminal-emulator
```

at the console. Choose xfce and quit. Restart the rdp connection and you should be fine.

To be able to monitor the Raspberry, I still installed my health module. Please follow the instructions in this repository:

https://github.com/jegali/HealthPi

To make sure the GPIO pins will repond correctly when addressed, I installed the new LGPIO library:

```bash
sudo apt install python3-lgpio
```

If you want to install k3s on the nodes (and we want) you can find the command on the K3s website. Be sure to have curl installed!

```bash
sudo apt install curl
```

Ubuntu admitted they have a bug in the current release preventing the node to get active. Thankfully there is a package that can be installed. Please be patient, it will take some time to install, to backup and to reboot:

```bash
sudo apt install linux-modules-extra-raspi
sudo reboot
```

## Changes to the firmware to make the hardware panel work
The really interesting problems always occur when you think you have everything installed. So I had connected my hardware panel to the Raspberry, but the LEDs did not light up. After a long research I then found out that by default under Ubuntu 21 the Serial Console is disabled - via this communicates GPIO pin 14 (TxD), and there is also the LED connected. The solution to the mystery: The line enable_uart=1 must be added to the file /boot/firmware/config.txt

```bash
[all]
kernel=vmlinuz
enable_uart=1
cmdline=cmdline.txt
initramfs initrd.img followkernel
```

Attention: In a Raspian installation you will find the config.txt file directly in the /boot directory. This directory and the file also exist under ubuntu - but you have to adjust the version under /boot/firmware!


## Customization on any device
This brings us to the end of the installation of Ubuntu. Now the SD card can be cloned and inserted into the other Raspberry. I recommend - to avoid confusion - to boot each Raspberry one after the other and to set the name on the command line:

```bash
sudo hostnamectl set-hostname minion01 
```

Luckily, I did not had to set the IP settings in ubuntu but could use my fritzBox Interface, so this concludes the preparation for the cluster installation.
