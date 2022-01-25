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



## Hardware Panel

I wanted to build a Hardware Panel to show the Raspberry's status and to be able to conveniently power on/off the devices. This section shows the development.

[Part 5: Hardware Panel](https://github.com/jegali/Cloudberry-Cluster/blob/main/hardware-panel.md)<br/>
<br/><br/>


This document describes how to set up a [lamp installation](https://github.com/jegali/Cloudberry-Cluster/blob/main/install-lamp.md)<br/>
This document describes how to set up a [reverse proxy](https://github.com/jegali/Cloudberry-Cluster/blob/main/reverse-proxy.md)<br/>




curl -sfL https://get.k3s.io | sh -
# Check for Ready node,
takes maybe 30 seconds
k3s kubectl get node
```


