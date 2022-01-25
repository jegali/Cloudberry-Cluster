# Architecture and Infrastructure
After the decision for the hardware was made, it was time to implement the architecture. The image below shows the infrastructure of the project. 

The Raspberry were installed with ubuntu and cloned eight times. I'll go into the installation process in a bit more detail in a moment. After that, the Raspberrys were individually connected to the switch, the hostname was set, the IP was assigned via my Fritzbox and the basic structure of the cluster is ready for use.

![Infrastructure](/images/cloudberry-infrastructure.png)

## Physical architecture

### Master Node: HP Slice
The HP Slice will become the master node. This box is equipped with 32 GB of RAM and an installation of Ubuntu 21 and later, an NGinx load balancer and redirector will be installed here, as well as the Kubernetes master plane. This node will get the IP address 192.168.178.29.

### Slave Nodes: Raspberry Pi 4
