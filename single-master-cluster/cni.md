# install flannel

```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

## install calico

```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

(option)

```
sudo -E kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
sudo -E kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml
```
