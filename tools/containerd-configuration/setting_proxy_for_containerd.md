# How to set proxy for containerd 
if you want to pull the images through a proxy you should follow below steps.

```bash
mkdir -p /etc/systemd/system/containerd.service.d
cat <<EOF > /etc/systemd/system/containerd.service.d/http-proxy.conf
[Service]
Environment="HTTP_PROXY=http://proxy.example.com"
Environment="HTTPS_PROXY=http://proxy.example.com"
Environment="NO_PROXY=localhost"
EOF
```
### Restart the necessary services 
```bash 
sudo systemctl daemon-reload
sudo systemctl restart containerd
sudo systemctl show --property=Environment containerd
```