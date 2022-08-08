Create config.yaml

```
mkdir -p /etc/rancher/rke2 && nano /etc/rancher/rke2/config.yml
```


Install rancherd

```
curl -sfL https://get.rancher.io | INSTALL_RANCHERD_VERSION=v2.5.8 sh -
```

Enavle services
```
systemctl enable rancherd-server.service
systemctl start rancherd-server.service
```

Check progress

```
journalctl -eu rancherd-server -f
```

Get kubeconfig (optional)
```
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml PATH=$PATH:/var/lib/rancher/rke2/bin
```

Verify running
```
kubectl get daemonset rancher -n cattle-system
kubectl get pod -n cattle-system
```

Set rancher password
```
rancherd reset-admin
```

```
hostAliases:
      - ip: 192.168.30.1
        hostnames:
        - "rancher.local"
```


```
kubectl -n cattle-system patch  deployments cattle-cluster-agent --patch '{
    "spec": {
        "template": {
            "spec": {
                "hostAliases": [
                    {
                      "hostnames":
                      [
                        "rancher.local"
                      ],
                      "ip": "192.168.30.1"
                    }
                ]
            }
        }
    }
}'

kubectl -n cattle-system patch  daemonsets cattle-node-agent --patch '{
 "spec": {
     "template": {
         "spec": {
             "hostAliases": [
                 {
                    "hostnames":
                      [
                        "rancher.local"
                      ],
                    "ip": "192.168.30.1"
                 }
             ]
         }
     }
 }
}'
```

