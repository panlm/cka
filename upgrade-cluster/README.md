# upgrade master node 1.20.1 --> 1.20.2

``` sh
sudo apt install --allow-change-held-packages kubeadm=1.20.2-00
kubectl drain control-node --ignore-daemonset
sudo kubeadm upgrade plan v1.20.2
sudo kubeadm upgrade apply v1.20.2

sudo apt install --allow-change-held-packages kubelet=1.20.2-00 kubectl=1.20.2-00
sudo systemctl daemon-reload
sudo systemctl restart kubelet
kubectl uncordon control-node

sudo apt-mask hold kubeadm kubelet kubectl

```


# upgrade worker node 1.20.1 --> 1.20.2

## on master node

``` sh
kubectl drain worker-node --ignore-daemonset
```

## on worker node

``` sh
sudo apt install --allow-change-held-packages kubeadm=1.20.2-00
sudo kubeadm upgrade node

sudo apt install --allow-change-held-packages kubelet=1.20.2-00 kubectl=1.20.2-00
sudo systemctl daemon-reload
sudo systemctl restart kubelet

sudo apt-mask hold kubeadm kubelet kubectl
```

## on master ndoe

``` sh
kubectl uncordon worker-node
```




