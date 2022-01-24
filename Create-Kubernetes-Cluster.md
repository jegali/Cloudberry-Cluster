# Setting up the kubernetes cluster

Setting up the cluster consists of two main parts: setting up the master, and setting up the nodes

## Setting up the master
To set up the master, we will follow the instructions shared on https://k3s.io/. This is nothing highly sophisticated, it just starts the server. Being the first node in the cluster, this no automatically becomes the master.

```bash
curl -sfL https://get.k3s.io | sh -
# Check for Ready node,
takes maybe 30 seconds
k3s kubectl get node
```

Please take the time and wait a minute before issuing the next command to see if the command worked:

```bash
sudo k3s server &
# Kubeconfig is written to /etc/rancher/k3s/k3s.yaml
sudo k3s kubectl get node
```

If we succeeded, we should see an output like this:

```
jens@aurorafox-ub:~$ sudo k3s kubectl get node
[sudo] Passwort für jens: 
NAME           STATUS   ROLES                  AGE   VERSION
aurorafox-ub   Ready    control-plane,master   27m   v1.22.5+k3s1
```

To connect a node to the just deployed server, you have to install k3s on the nodes as well, and you will have to provide a security token to the nodes. This security token is created during install of the master node and can be found in this file:

```bash
/var/lib/rancher/k3s/server/node-token
```

If you want to deploy more than one node, please consider constructing the command in notepad or notepad++ so you can easily copy and paste it.<br/><br/>


## Setting up the nodes

I deployed k3s before on a Raspberry with Ubuntu 20 without any issues. Ubuntu 21 throws an error "bind failed" or "address alerady in use". This is not a k3s issue, but a bug in Ubuntu 21. This bug can be fixed by installing these commands. Please be patient, it will take some time to install, to backup and to reboot:

```bash
sudo apt install linux-modules-extra-raspi
sudo reboot
```

After that, k3s can be installed with

```bash
curl -sfL https://get.k3s.io | K3S_URL=https://192.168.178.29:6443 K3S_TOKEN=K10f578728f969fb6f29557ca082c5abcd95edc3ee5a64ddeff94b3fef7a1c76d9f::server:be45bbb89faedfcc91cfcc78d4d1ab31 sh -
```

where 192.168.178.29 is my server's address. The token is the content of the file 

```bash
/var/lib/rancher/k3s/server/node-token
```

Please do not take the token offered here - it is a fake token. After installing the extra modules and installing the nodes, you can issue 

```bash
jens@aurorafox-ub:~$ sudo k3s kubectl get node
NAME           STATUS   ROLES                  AGE   VERSION
minion01       Ready    <none>                 64m   v1.22.5+k3s1
minion06       Ready    <none>                 63m   v1.22.5+k3s1
minion02       Ready    <none>                 65m   v1.22.5+k3s1
minion03       Ready    <none>                 63m   v1.22.5+k3s1
aurorafox-ub   Ready    control-plane,master   99m   v1.22.5+k3s1
minion08       Ready    <none>                 63m   v1.22.5+k3s1
minion07       Ready    <none>                 63m   v1.22.5+k3s1
minion04       Ready    <none>                 63m   v1.22.5+k3s1
minion05       Ready    <none>                 63m   v1.22.5+k3s1
jens@aurorafox-ub:~$ 
```

on the server. The nodes should go ready after short time.
