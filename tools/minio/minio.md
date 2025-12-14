# Minio Installation
First of all you must add the minio repository and update your helm repositories through below commands.
```bash
helm repo add minio https://charts.min.io/
helm repo update
```
Second of all, you must copy the current values to the "values.yml" in your system.
```bash
helm show values minio/minio > values.yml
```
## NOTE
Necessary environment which should be considered are as follows.
| Item              | In Stock | Price |
| :---------------- | :------: | ----: |
| rootUser | #Replace it with your desired values |
| rootPassword | #Replace it with your desired values |
| replicas | #update this value with the number of pod |
| persistence.size | #default is 10Gi |
