# Cloudberry-Cluster
In this repository, I show how I built my raspberry Kubernetes cluster - including a small hardware project that deals with creating a front panel with LED and on/off switches so that the cluster can be conveniently started and shut down. The first part deals with the hardware requirements. The second part goes into with the creation of the panel. In part three I discuss the software installation on the 8 Raspberry Computers.<br/><br/>

## Hardware Requirements
I wanted to make the work for this project as pleasant as possible. In particular, I wanted to have a way to shut down the cluster for vacation periods and be able to restart it just as conveniently. The whole thing should be possible without having to log in to each Raspberry every time and manually shutting down the Raspberry. Because as we all know - simply cutting the power and stopping the Raspberry in this way can corrupt the SD card and thus severely affect the further functioning of the Raspberry.<br/><br/>
Neither did I want eight small power supplies in my room in a multiple socket. So I decided to equip the Raspberry with a Power over Ethernet (PoE) Hat to be able to guarantee the power supply via a switch. As far as both the PoE hats and the switch were concerned, it took several iterations before I was satisfied with the result. 

### Iteration 1:
I bought a small kit to stack the Raspberry with. A good idea for my very first experiment with four Raspberry. For building the cluster too small and a little too ... unspectacular. <br/><br/>

https://www.amazon.de/GeeekPi-Raspberry-Transparent-Stapelbarer-K%C3%BChlk%C3%B6rper/dp/B07Z4GRQGH/ref=sr_1_5?keywords=raspberry+cluster+case&qid=1643012204&sprefix=raspberry+cluster%2Caps%2C82&sr=8-5

https://www.amazon.de/GeeekPi-Raspberry-Cluster-Stapelbares-12-Lagen/dp/B08FHJ5TR2/ref=sr_1_10?keywords=raspberry+cluster+case&qid=1643012141&sprefix=raspberry+cluster%2Caps%2C82&sr=8-10
