# Multi Master (HA) k3os Virtualbox vagrant setup

## Details

K3os is a Linux Distribution (https://github.com/rancher/k3os) designed to run k3s.

This vagrant setup will launch three k3s virtualbox master servers to allow for control plane HA. The default setup uses k3s Dqlite https://dqlite.io/docs/ for clustering.

## Quick Start

``$>vagrant up``

Once the boxes are loaded

`$>vagrant ssh server1`
`$>kubectl get nodes`

```
    NAME                        STATUS   ROLES    AGE     VERSION
k3s-server-01.cluster.k3s   Ready    master   10m     v1.17.2+k3s1
k3s-server-02.cluster.k3s   Ready    master   10m     v1.17.2+k3s1
k3s-server-03.cluster.k3s   Ready    master   9m26s   v1.17.2+k3s1
```

## Tested in

Ubuntu 18.04LTS
Vagrant 2.2.7
Virtualbox 6.1

## Networking

In order for the clusters to be able to communicate the mac addresses of the interfaces for the machines have been assigned and k3os configured via conman to configure the ip addresses.

This can be modified by altering config/server[number]/k3os/config.yaml

 - server1 = 192.168.1.115
 - server2 = 192.168.1.116
 - server2 = 192.168.1.117

Both the boot_cmd and k3_args should be updated if any ip address changes.