### Setting up Rook
First of all you must make sure 'LVM' is installed on all the servers.

### Clone the Repository

```bash
git clone --single-branch --branch release-1.3 https://github.com/rook/rook.git
```
Now enter the directory using the following command 

``` bash
cd rook/deploy/examples
````
Next you will continue by creating the common resources you needed for your Rook deployment, which you can do by deploying the Kubernetes config file that is available by default in the directory

``` bash
kubectl create -f common.yaml
```
In this stage, apply the 'operator.yaml' manifest inside your cluster. Before applying it, have a look and modify necessary items.

```bash
kubectl create -f operator.yaml
```

Make sure all the pods are in the state of 'Up & Running'.
```bash
kubectl get pod -n rook-ceph
```

### Creating a Ceph Cluster

In the manifest examples directory, there is 'cluster.yaml' file which is responsible to create a ***Ceph*** cluster inside the kubernetes, make sure that all the values are suitable based on your env before applying it.

```bash
kubectl apply -f cluster.yaml
```

it takes a while based on your network speed and situtation untill all the pods get running.

```bash
kubectl get pod -n rook-ceph
```

### Adding Block Storage

Before Ceph can provide storage to your cluster, you first need to create a storageclass and a cephblockpool. This will allow Kubernetes to interoperate with Rook when creating persistent volumes
```bash
kubectl apply -f ./csi/rbd/storageclass.yaml
```

in order to test if your storage clase (dynamic provisioning) is working properly, create a PVC inside your cluster.

```bash
vi pvc-rook-ceph-block.yaml
```
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pvc
spec:
  storageClassName: rook-ceph-block
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```
Then apply your manifest in the kubernetes cluster using the command below.
```bash
kubectl apply -f pvc-rook-ceph-block.yaml
```
Make sure that your PVC is bound

```bash
kubectl get pvc
```
