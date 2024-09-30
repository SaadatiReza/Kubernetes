# Install RKE2
First, execute the script below to install the necessary services:

```bash
curl -sfL https://get.rke2.io | sh -
```
Then, enable the RKE2 service with the following command:

```bash
systemctl enable rke2-server.service
```

If you prefer to continue setting up and running your RKE2 cluster with the default configuration, you can skip the following steps.

Otherwise, create a configuration directory and file:
```bash

mkdir -p /etc/rancher/rke2/
vim /etc/rancher/rke2/config.yaml
#The first two lines in the file are not required for initializing your cluster. They are useful for joining other nodes (servers or agents).
token: # You can find the token after the first server initializes successfully at this location: "/var/lib/rancher/rke2/server/node-token"
server: https://192.168.56.11:9345 # This is the address of your first master node.

# Keep in mind that the SANs are necessary for Kubernetes communication. Add the addresses of all your nodes here.
tls-san:
  - 192.168.56.20
  - 192.168.56.11
  - 192.168.56.12
  - 192.168.56.13

# If you are using multiple network adapters and want to set a specific one as your default, define its IP address here.
node-ip: 192.168.56.11

# RKE2 uses CANAL CNI for pod communication by default. If you want to change the default CNI, specify the key and value below.
cni: calico
```
it's time to RUN your cluster through starting the rke2 service with the below command
```bash
systemctl start rke2-server.service
#depending on your system hardware and network internet connection it takes a time be be loaded successfully.
journalctl -u rke2-server -f
```
Repeat this process for each RKE2 server you have, to join them to the existing cluster


### Join your Agent

Similar to the steps for creating the cluster, we need to install the necessary packages and services on the agents using the script below:

```bash
curl -sfL https://get.rke2.io | INSTALL_RKE2_TYPE="agent" sh -
```

Unlike the server node, where having a config file is optional, for joining agents you **must** create a config file and specify the server address and token.

```bash
mkdir -p /etc/rancher/rke2/
vim /etc/rancher/rke2/config.yaml
# Place the configuration below in your config file
server: https://<server>:9345
token: <token from server node>
```

### Start the Agent Service

To start the agent service, run the following command:

```bash
systemctl start rke2-agent.service
```

