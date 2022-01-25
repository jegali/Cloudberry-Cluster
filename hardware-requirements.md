# Hardware Requirements
I wanted to make the work for this project as pleasant as possible. In particular, I wanted to have a way to shut down the cluster for vacation periods and be able to restart it just as conveniently. The whole thing should be possible without having to log in to each Raspberry every time and manually shutting down the Raspberry. Because as we all know - simply cutting the power and stopping the Raspberry in this way can corrupt the SD card and thus severely affect the further functioning of the Raspberry.<br/><br/>
Neither did I want eight small power supplies in my room in a multiple socket. So I decided to equip the Raspberry with a Power over Ethernet (PoE) Hat to be able to guarantee the power supply via a switch. As far as both the PoE hats and the switch were concerned, it took several iterations before I was satisfied with the result. 



## The first cluster case

I bought a small kit to stack the Raspberry with. A good idea for my very first experiment with four Raspberry. For building the cluster too small and a little too ... unspectacular. <br/>

<img src="https://m.media-amazon.com/images/I/71bLVe56y6L._AC_SL1490_.jpg" width="30%">

https://www.amazon.de/GeeekPi-Raspberry-Transparent-Stapelbarer-K%C3%BChlk%C3%B6rper/dp/B07Z4GRQGH/ref=sr_1_5?keywords=raspberry+cluster+case&qid=1643012204&sprefix=raspberry+cluster%2Caps%2C82&sr=8-5



## The second cluster case


So I decided to get a case that would give me space and also be able to withstand expansion requests for a while. Space for 12 Raspberry should be enough for now.

<img src="https://m.media-amazon.com/images/I/61qsgLvszbL._AC_SL1000_.jpg" width="30%">

https://www.amazon.de/GeeekPi-Raspberry-Cluster-Stapelbares-12-Lagen/dp/B08FHJ5TR2/ref=sr_1_10?keywords=raspberry+cluster+case&qid=1643012141&sprefix=raspberry+cluster%2Caps%2C82&sr=8-10



## The sound of silence

I still decided to swap the installed fans for Mirage 12 Pro from AeroCool. More color, more silence  - but I needed a second power line, which the Raspberry could not provide and had to install and bridge a PC switching power supply. And the project grew and grew....

<img src="https://m.media-amazon.com/images/I/81AKTs583dL._AC_SL1500_.jpg" width="30%">

https://www.amazon.de/AeroCool-MIRAGE12PRO-L%C3%BCfter-120mm-ger%C3%A4uschlos/dp/B08DL4J4C7/ref=sr_1_1?keywords=mirage%2B12%2Bpro&qid=1643012711&sprefix=mirage%2B12%2B%2Caps%2C70&sr=8-1&th=1



## You can leave your hat on

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
