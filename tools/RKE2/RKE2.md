#Install RKE2
firstly, you should execute the below script install necesssary services.

```bash
curl -sfL https://get.rke2.io | sh -
```
then enable the rke2 service with the below command.
```bash
systemctl enable rke2-server.service
```

if you prefer continue set up and runn your rke2 cluster with the default value, skip the below steps.
```bash

mkdir -p /etc/rancher/rke2/
vim /etc/rancher/rke2/config.yaml
#two lines from begining are not necessary for the initialization of your cluster and they are useful for joining other server(including servers and agents).
token: #you can find the token once the first server has been initialized successfully at the following location "/var/lib/rancher/rke2/server/node-token"
server: https://192.168.56.11:9345 #this is the address of your first master node.
#keep in mind that the sans are necessary in the kubernetes communication, try to add all of your nodes address into this part.
tls-san:
  - 192.168.56.20
  - 192.168.56.11
  - 192.168.56.12
  - 192.168.56.13
#if you're using multiple network adapter and prefer to use one of them as your default network adapter try to define its address in this place.
node-ip: 192.168.56.11
#RKE2 uses CANAL CNI for communication of your pod by default, if you want to change your default cni try to define below key value.
cni: calico
```
it's time to RUN your cluster through starting the rke2 service with the below command
```bash
systemctl start rke2-server.service
#depending on your system hardware and network internet connection it takes a time be be loaded successfully.
journalctl -u rke2-server -f
```



