# Setting up the kubernetes cluster

Setting up the cluster consists of two main parts: setting up the master, and setting up the nodes

## Setting up the master
To set up the master, we will follow the instructions shared on https://k3s.io/. This is nothing highly sophisticated, it just starts the server. Being the first node in the cluster, this no automatically beomces the master.

```bash
curl -sfL https://get.k3s.io | sh -
# Check for Ready node,
takes maybe 30 seconds
k3s kubectl get node
```
