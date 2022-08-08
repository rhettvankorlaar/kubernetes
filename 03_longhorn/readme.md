Step 1

```
sudo apt-get install nfs-common open-iscsi util-linux
```


Step 2 Install and update repo

```
helm repo add longhorn https://charts.longhorn.io && helm repo update
```

Step 3

```
helm install longhorn longhorn/longhorn --namespace longhorn-system --create-namespace
```


