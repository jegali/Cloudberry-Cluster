# Cloudberry-Cluster
In this repository, I show how I built my raspberry Kubernetes cluster - including a small hardware project that deals with creating a front panel with LED and on/off switches so that the cluster can be conveniently started and shut down. I have divided the document into several parts in order to keep it clear and to be able to offer the reader targeted sections in which he is interested.<br/><br/>


## Hardware Requirements

In this section, you'll learn about the hardware requirements that came up for the project. In particular, I want to write about the stumbling blocks in hardware selection, since this was associated with avoidable costs for me - and you don't have to make these mistakes over and over again, do you?

[Part 1: Hardware Requirements](https://github.com/jegali/Cloudberry-Cluster/blob/main/hardware-requirements.md)<br/>
<br/><br/>


## Architecture and Infrastructure

This section shows the hardware architecture. Closely related to the actual physical structure is the cluster architecture, which I will also present in this section.

[Part 2: Architecture and Infrastructure](https://github.com/jegali/Cloudberry-Cluster/blob/main/architecture.md)<br/>
<br/><br/>



## Raspberry install and configuration

I divided the installation of the raspberry and kubernetes into two separate sections. This section deals with the Raspberry installation.

[Part 3: Ubuntu install](https://github.com/jegali/Cloudberry-Cluster/blob/main/ubuntu-install.md)<br/>
<br/><br/>



## Kubernetes install and configuration

I divided the installation of the raspberry and kubernetes into two separate sections. This section deals with the kubernetes installation.

[Part 4: Kubernetes cluster](https://github.com/jegali/Cloudberry-Cluster/blob/main/Create-Kubernetes-Cluster.md)<br/>
<br/><br/>


This document describes how to set up a [lamp installation](https://github.com/jegali/Cloudberry-Cluster/blob/main/install-lamp.md)<br/>
This document describes how to set up a [reverse proxy](https://github.com/jegali/Cloudberry-Cluster/blob/main/reverse-proxy.md)<br/>





curl -sfL https://get.k3s.io | sh -
# Check for Ready node,
takes maybe 30 seconds
k3s kubectl get node
```




# Building of the Hardware Panel
As discussed earlier, I wanted to build a Hardware Panel to show the Raspberry's status and to be able to conveniently power on/off the devices. The following picture shows the panel in action.

![panel-1](/images/panel-1.png)

For the creation of the panel again some hardware was necessary. I needed an aluminum strip, some pushbuttons, LEDs, the necessary series resistors, cables and sockets for the LEDs.

In times of pandemic and closed stores, amazon is really a winner, so of course it's no surprise when I bought the components there. Aluminum strips are there in all colors and shapes, I chose a strip 40x20x1000mm, which still had to be cut to size afterwards

<img src="https://m.media-amazon.com/images/I/51Kr8StbFMS._AC_SL1500_.jpg" width="30%">

https://www.amazon.de/gp/product/B003ZUL9S4/ref=ppx_yo_dt_b_search_asin_image?ie=UTF8&psc=1

I bought light emitting diodes directly together with resistors, after I had calculated the required series resistance. This complete package left nothing to be desired

<img src="https://m.media-amazon.com/images/I/71PhkLcEYJL._AC_SL1001_.jpg" width="30%">

https://www.amazon.de/gp/product/B07YWX42RJ/ref=ppx_yo_dt_b_search_asin_image?ie=UTF8&psc=1

To be able to fit the LEDs well, I treated myself to some more sockets

<img src="https://m.media-amazon.com/images/I/61Q4f5NAAgL._AC_SL1001_.jpg" width="30%">

https://www.amazon.de/gp/product/B075H9GJHF/ref=ppx_yo_dt_b_search_asin_image?ie=UTF8&psc=1

I found the necessary buttons to switch on and off here

<img src="https://m.media-amazon.com/images/I/61sPc1mLqTL._AC_SL1000_.jpg" width="30%">

https://www.amazon.de/gp/product/B081JJBN4G/ref=ppx_yo_dt_b_search_asin_image?ie=UTF8&psc=1

Of course, for tinkering you still need a soldering iron, ideally with a third hand and a little solder. But I see this rather as basic equipment and do not want to post more links here.

Using CorelDraw - a program I've been using for at least 30 years - I then drew and printed a layout of the switches and LEDs

![cluster-panel](/images/panel-2.png)

Fixed with scotch tape on the aluminum bar, the holes for the drilling could then be made with a center punch. Unfortunately, I didn't have much experience with machining aluminum, and using the metal drill available to me didn't produce the desired results.

![cluster-panel](/images/panel-3.jpg)

A visit to youTube Academy showed me that I should use a step drill. So ordered another step drill from Amazon and re-drilled the holes. And lo and behold - this time the holes were round and usable.

<img src="https://m.media-amazon.com/images/I/71I6Hbm5WkL._AC_SL1500_.jpg" width="30%">

https://www.amazon.de/gp/product/B001Q3LY1E/ref=ppx_yo_dt_b_search_asin_image?ie=UTF8&psc=1

![cluster-panel](/images/panel-4.jpg)

The last time I soldered was about 30 years ago - accordingly, the first solder joint was also directly cold and broke. Here, too, a visit to the youTube Academy was worthwhile to refresh my rusty knowledge. After a few tentative attempts, soldering worked quite well again.

![cluster-panel](/images/panel-5.jpg)

And so it did not take long until the panel was completely soldered and assembled in front of me. 

![cluster-panel](/images/panel-6.jpg)

## Calculation of the resistor for the circuit

What I also didn't remember was the calculation of the series resistor for the LED circuit. So that I do not forget it this time again, I write down the procedure here.

The task is to make an LED light up on a Raspberry Pi. This is not very difficult. We need an LED (no matter what color), a resistor whose value still has to be calculated, a Raspberry Pi, preferably a plug-in board and connecting cables from the GPIO pins to the plug-in board.


In principle, you should never connect an LED directly between 3.3 V and GND. This can work well, but it does not have to. You have to know that LEDs have a fixed operating voltage, which is below 3.3 V and it also needs a current limiter, because otherwise they draw too much current, which causes them to self-destruct. Both the voltage and the current are controlled by a series resistor, the value of which depends on the excess voltage and the desired current through the light emitting diode.
It is also necessary to take into account that an LED has two different poles. So you have to pay attention to how around the LED is installed in the circuit.

In the following we will deal with how the LED is polarized and how the series resistor is calculated.

![cluster-panel](/images/circuit-panel-gpio.gif)

For the LED to light up, the GPIO "internal" must be switched to "high" (1). Only then a current flows through the LED.
To calculate the forward resistance we need two values. One value is the forward voltage U_F of the LED and the other value is the forward current I_F of the LED. Normally you can get these values from the datasheet of the LED.
If you don't have the data sheet of the LED or these values are unknown, then you have to find them out by experimenting.

We use an LED with 2.0 V and 20 mA (0.02 A) as an example. However, the 20 mA is the maximum value. This LED also lights up at 10 mA. Not quite as bright, but sufficiently visible. Therefore we take a value of 10 mA for the LED forward current.

![cluster-panel](/images/calculate-resistor.png)

The series resistance is calculated using Ohm's law. Here, a voltage is divided by the current, resulting in a resistor value. The voltage that must drop across the resistor is the total voltage (3.3 V) minus the LED forward voltage (2.0 V). The result (1.3 V) is divided by the LED forward current (10 mA) to get the value for the series resistor (130 Ohm).
Now, unfortunately, this value is not available as a component, so you have to take a slightly smaller or larger value. According to the E-series E12 the next smaller value is 120 Ohm. The next larger value is 150 Ohm. As a rule, one takes the larger value. I took a resistor value of 220 Ohm.

How to connect an LED correctly? Typically, the two connecting wires of an LED are of different lengths. The longer of the two is the anode (positive pole). The shorter one is the cathode (negative pole).
Easy to remember: The plus sign has one more dash than the minus sign, making the wire slightly longer. Also, most LEDs are flattened on the minus side, like a minus, or the "K" of the cathode.

With the circuit symbol, you can remember it like this. There, the circuit symbol has the shape of the letter "K" because of the crossbar. The triangle is similar to the letter "A". In the case of the crossbar, the terminal is the cathode and on the other side is the anode. The anode points away from the positive pole to the negative pole, indicating the direction of current. From plus to minus. And thus the anode is connected to the positive pole and the cathode to the negative pole.
