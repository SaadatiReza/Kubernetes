
# NFS-StorageClass Server Configuration

First of all, you should install the nfs server on one of your server. best practices emphasizes to install on a seprate machine from your cluster.


```bash
  sudo apt update
  sudo apt install nfs-kernel-server
  #this place is going to be your saving place. try to modify it as per your case.
  sudo mkdir -p /mnt/nfs_share
  sudo chown -R nobody:nogroup /mnt/nfs_share/
  sudo chmod 777 /mnt/nfs_share/
  sudo vi /etc/exports
```


Add the below content in your /etc/exports file. (Don't forget to change the Address of your client. replace "10.0.2.15/24" with your desired network.)
```bash
/mnt/nfs_share 10.0.2.15/24(rw,sync,no_subtree_check)
```
Utilize the provided command for exporting the NFS shared directory and restart the service
 ```bash
 sudo exportfs -a
 sudo systemctl restart nfs-kernel-server
 ```


# NFS-StorageClass Client Configuration
Install the below packages on all of your node (sudo apt install nfs-common)

```bash
sudo apt install nfs-common
```

# Install NFS Subdir External Provisioner with HELM
Now, you must install NFS Provisioner inside your kubernetes cluster to automate the procedures of dynamic provisioning.
```bash
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/

helm install nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
    --set nfs.server=x.x.x.x \
    --set nfs.path=/exported/path
```
replace the value of **"nfs.server"** with your NFS server address and **"nfs.path"** with your nfs directory (in this case is /mnt/nfs_share/)

If you want it to make this Storage Class as your default storage class use the below command.

```bash
kubectl patch storageclass nfs-client -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```
