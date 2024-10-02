# Installation RKE2 In an AirGap environment
Based on the official documentation of RKE2, there are different ways of installing RKE2 cluster in an environment where doesn't have any direct access to Internet.
In this scenario, we're going to cover the method which RKE2 will be installed through running the "Install.sh" script.

First, download the all necessary file and move to your target machine.
```bash
mkdir /root/rke2-artifacts && cd /root/rke2-artifacts/
curl -OLs https://github.com/rancher/rke2/releases/download/v1.26.10%2Brke2r2/rke2-images.linux-amd64.tar.zst
curl -OLs https://github.com/rancher/rke2/releases/download/v1.26.10%2Brke2r2/rke2.linux-amd64.tar.gz
curl -OLs https://github.com/rancher/rke2/releases/download/v1.26.10%2Brke2r2/sha256sum-amd64.txt
curl -sfL https://get.rke2.io --output install.sh
```
consider chaning the address regarding the version that you're looking to install.
```INSTALL_RKE2_ARTIFACT_PATH=/root/rke2-artifacts bash -x install.sh```
Then, if you have any further configuration make sure that put them in the proper location .
```bash
mkdir -p /etc/rancher/rke2/
vim /etc/rancher/rke2/config.yaml
```
You should enable and start the service.
```bash
systemctl enable rke2-server.service
systemctl start rke2-server.service
journalctl -u rke2-server -f
```

