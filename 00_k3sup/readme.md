Install master

```
k3sup install --ip 192.168.40.1 --user root --k3s-extra-args "--write-kubeconfig-mode 644 --disable servicelb --disable traefik --bind-address 192.168.40.1 --disable local-storage" --k3s-version v1.21.11+k3s1
```

Install node

```
k3sup join --ip 192.168.50.1 --user root --server-ip 192.168.40.1 --k3s-version v1.21.11+k3s1
```

Transfer Kubeconfig

```
scp root@192.168.40.1:/etc/rancher/k3s/k3s.yaml ~/.kube/config && chmod 600 ~/.kube/config
```