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
