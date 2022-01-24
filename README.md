# Cloudberry-Cluster
In this repository, I show how I built my raspberry Kubernetes cluster - including a small hardware project that deals with creating a front panel with LED and on/off switches so that the cluster can be conveniently started and shut down. The first part deals with the hardware requirements. The second part goes into with the creation of the panel. In part three I discuss the software installation on the 8 Raspberry Computers.<br/><br/>

## Hardware Requirements
I wanted to make the work for this project as pleasant as possible. In particular, I wanted to have a way to shut down the cluster for vacation periods and be able to restart it just as conveniently. The whole thing should be possible without having to log in to each Raspberry every time and manually shutting down the Raspberry. Because as we all know - simply cutting the power and stopping the Raspberry in this way can corrupt the SD card and thus severely affect the further functioning of the Raspberry.<br/><br/>
Neither did I want eight small power supplies in my room in a multiple socket. So I decided to equip the Raspberry with a Power over Ethernet (PoE) Hat to be able to guarantee the power supply via a switch. As far as both the PoE hats and the switch were concerned, it took several iterations before I was satisfied with the result. 

### Iteration 1:
I bought a small kit to stack the Raspberry with. A good idea for my very first experiment with four Raspberry. For building the cluster too small and a little too ... unspectacular. <br/>

<img src="https://m.media-amazon.com/images/I/71bLVe56y6L._AC_SL1490_.jpg" width="30%">

https://www.amazon.de/GeeekPi-Raspberry-Transparent-Stapelbarer-K%C3%BChlk%C3%B6rper/dp/B07Z4GRQGH/ref=sr_1_5?keywords=raspberry+cluster+case&qid=1643012204&sprefix=raspberry+cluster%2Caps%2C82&sr=8-5

So I decided to get a case that would give me space and also be able to withstand expansion requests for a while. Space for 12 Raspberry should be enough for now.

<img src="https://m.media-amazon.com/images/I/61qsgLvszbL._AC_SL1000_.jpg" width="30%">

https://www.amazon.de/GeeekPi-Raspberry-Cluster-Stapelbares-12-Lagen/dp/B08FHJ5TR2/ref=sr_1_10?keywords=raspberry+cluster+case&qid=1643012141&sprefix=raspberry+cluster%2Caps%2C82&sr=8-10

I still decided to swap the installed fans for Mirage 12 Pro from AeroCool. More color, more silence  - but I needed a second power line, which the Raspberry could not provide and had to install and bridge a PC switching power supply. And the project grew and grew....

<img src="https://m.media-amazon.com/images/I/81AKTs583dL._AC_SL1500_.jpg" width="30%">

https://www.amazon.de/AeroCool-MIRAGE12PRO-L%C3%BCfter-120mm-ger%C3%A4uschlos/dp/B08DL4J4C7/ref=sr_1_1?keywords=mirage%2B12%2Bpro&qid=1643012711&sprefix=mirage%2B12%2B%2Caps%2C70&sr=8-1&th=1

Now the PoE hats came into play. I bought 8 PoE Hats from Waveshare - really great little parts. Unfortunately I had not considered the height, so I could only use 6 of the 12 slots in my cluster enclosure

<img src="https://m.media-amazon.com/images/I/61C2zig-gHL._AC_SL1500_.jpg" width="30%">

https://www.amazon.de/Waveshare-HAT-Raspberry-PoE-Switched-Mode/dp/B07H95Z21P/ref=sr_1_3?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=IX115247RQS3&keywords=waveshare%2Bpoe&qid=1643014362&sprefix=waveshare%2Bpoe%2Caps%2C55&sr=8-3&th=1

So I gave it a try with the original PoE hats from Raspberry. So finally all Raspberry fit again in the cluster case.

<img src="https://m.media-amazon.com/images/I/71mCQZq9z6L._AC_SL1500_.jpg" width="30%">

https://www.amazon.de/Raspberry-Pi-Foundation-PoE-Netzteil/dp/B07GR9XQJH/ref=sr_1_4?keywords=raspberry+poe+hat&qid=1643014446&sprefix=raspberry+poe%2Caps%2C63&sr=8-4

But what I couldn't overlook at this stage of my project: the GPIO pins are not passed through, so there would be no way to attach a status LED and/or an on/off switch....
So I invested again and bought more PoE Hats. This time again from Waveshare, but with (mostly) free access to the GPIO strip. Mostly because exactly pin 3 and pin 4 were covered by the hat again, which I saw too late...

<img src="https://m.media-amazon.com/images/I/61zjM9eo4mS._AC_SL1500_.jpg" width="30%">

https://www.amazon.de/PoE-HAT-802-3af-Konform-DC-Ausgang-Offiziellen/dp/B092VVFKWT/ref=sr_1_1_sspa?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=33QX069WCZ6KI&keywords=raspberry%2Bpoe%2Bhat&qid=1643014707&sprefix=raspberry%2Bpoe%2Bhat%2Caps%2C71&sr=8-1-spons&smid=A3CMRZVKHXMDH4&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUExUzJXTlJaMEJYNkhRJmVuY3J5cHRlZElkPUEwNDgyOTY0MUNaUkJRR1YxQ0pSTiZlbmNyeXB0ZWRBZElkPUEwNjQyODQ1M0JNVUJaT0oyUFFFOCZ3aWRnZXROYW1lPXNwX2F0ZiZhY3Rpb249Y2xpY2tSZWRpcmVjdCZkb05vdExvZ0NsaWNrPXRydWU&th=1

As a result, I restructured the project a little bit. The PoE-capable but unmanaged Netgear switch I bought was replaced with a managed switch. However, the switches with 16 ports become outrageously expensive, I have unfortunately no comparison, but may also be due to the current supply shortages due to the corona pandemic. In any case, I purchased a switch from Zyxel, which meets my needs for now. 8 PoE ports and two ports that can be used as uplink. My security-savvy heart started beating a little irregularly when I read in the manual that the credentials are admin and 1234. 2022...

<img src="https://m.media-amazon.com/images/I/61o-iMe7XvL._AC_SL1000_.jpg" width="30%">

https://www.amazon.de/gp/product/B0189ZRSMK/ref=ppx_yo_dt_b_asin_image_o06_s00?ie=UTF8&th=1

As mentioned before, I didn't want to have 8 switching power supplies lying around in my study, and from my older experiments with Raspberry I only remembered rigid, unbendable network cables, so for this experiment I equipped myself with flat, PoE capable, network cables.

<img src="https://m.media-amazon.com/images/I/61cXt0r2+1L._AC_SL1300_.jpg" width="30%">

https://www.amazon.de/gp/product/B08R3YRPMB/ref=ppx_yo_dt_b_search_asin_image?ie=UTF8&psc=1


## Infrastructure
After the decision for the hardware was made, it was time to implement the architecture. The image below shows the infrastructure of the project. 

The Raspberry were installed with ubuntu and cloned eight times. I'll go into the installation process in a bit more detail in a moment. After that, the Raspberrys were individually connected to the switch, the hostname was set, the IP was assigned via my Fritzbox and the basic structure of the cluster is ready for use.

![Infrastructure](/images/cloudberry-infrastructure.png)


## Raspberry Installation
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
