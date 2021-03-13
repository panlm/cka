# setup ubuntu + containerd environment

## setup kubernetes cluster

* download image from [HERE](https://cloud-images.ubuntu.com/bionic/current/bionic-server-cloudimg-amd64.img)
* using cloud-init to setup default user `nutanix` and it's default password. (You should know that if using nutanix products.)

```
#cloud-config
disable_root: False
ssh_enabled: True
ssh_pwauth: True
users:
  - name: nutanix
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
    lock-passwd: false
    passwd: $6$4guEcDvX$HBHMFKXp4x/Eutj0OW5JGC6f1toudbYs.q.WkvXGbUxUTzNcHawKRRwrPehIxSXHVc70jFOp3yb8yZgjGUuET.
```

* remeber to resize boot disk after you create the VM.
* using [ubuntu-containerd.sh](./ubuntu-containerd.sh) to setup
* on the first node (as master)
  * modify `/tmp/init`, change ip address and node register name
  * create master node

  ```
  sudo kubeadm init --config /tmp/init
  ```

* on the others node (as worker)
  * modify `/tmp/join`, change master ip and node register name
  * create worker node

  ```
  sudo kubeadm join --config /tmp/join
  ```

## install network cni

you could choose `flannel` or `calico`

### install flannel

```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

### install calico

```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

(option)

```
kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml
```

## Others

### nfs-client

install nfs-client if you try to play around with it

`sudo apt install -y nfs-client`


# setup centos + docker environment

* download image from [HERE](https://cloud.centos.org/centos/7/images/CentOS-7-x86_64-GenericCloud-2009.qcow2)
* using cloud-init to setup default user `nutanix` and it's default password. (You should know that if using nutanix products.)

```
#cloud-config
disable_root: False
ssh_enabled: True
ssh_pwauth: True
users:
  - name: nutanix
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
    lock-passwd: false
    passwd: $6$4guEcDvX$HBHMFKXp4x/Eutj0OW5JGC6f1toudbYs.q.WkvXGbUxUTzNcHawKRRwrPehIxSXHVc70jFOp3yb8yZgjGUuET.
```



