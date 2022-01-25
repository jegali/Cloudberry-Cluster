# Architecture and Infrastructure
After the decision for the hardware was made, it was time to implement the architecture. The image below shows the infrastructure of the project. 

The Raspberry were installed with ubuntu and cloned eight times. I'll go into the installation process in a bit more detail in a moment. After that, the Raspberrys were individually connected to the switch, the hostname was set, the IP was assigned via my Fritzbox and the basic structure of the cluster is ready for use.

![Infrastructure](/images/cloudberry-infrastructure.png)

## Physical architecture

### Master Node: HP Slice
The HP Slice will become the master node. This box is equipped with 32 GB of RAM and an installation of Ubuntu 21 and later, an NGinx load balancer and redirector will be installed here, as well as the Kubernetes master plane. This node will get the IP address 192.168.178.29.

### Slave Nodes: Raspberry Pi 4
The Raspberry will also be equipped with Ubuntu 21. I plan to install only one node completely. I know that an external monitor (and a mouse and keyboard) will be needed at the beginning of the configuration, so I only want to do this installation process once to avoid having to constantly replug everything. Then openSSH and RDP will be installed to do the rest remotely. The IP addresses of the cluster will be:

* Minion 01: 192.168.178.101
* Minion 02: 192.168.178.102
* Minion 03: 192.168.178.103
* Minion 04: 192.168.178.104
* Minion 05: 192.168.178.105
* Minion 06: 192.168.178.106
* Minion 07: 192.168.178.107
* Minion 08: 192.168.178.108
