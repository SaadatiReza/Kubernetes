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

