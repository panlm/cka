# reference 

[LINK](https://kubernetes.io/zh/docs/tasks/configure-pod-container/configure-pod-configmap/#%E5%9C%A8-pod-%E5%91%BD%E4%BB%A4%E4%B8%AD%E4%BD%BF%E7%94%A8-configmap-%E5%AE%9A%E4%B9%89%E7%9A%84%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)

# labs

## create configmap

```
kubectl create cm kube-config --from-file=/etc/kubernetes/admin.conf \
  --from-literal=path=/etc/my-kube-config/admin.conf
```

## pod yaml

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-kubectl
spec:
  containers:
  - image: public.ecr.aws/bitnami/kubectl:latest
    name: pod
    command: ["sh","-c","kubectl get no -o wide ; sleep 3600"]
    env:
      - name: KUBECONFIG
        valueFrom:
          configMapKeyRef:
            name: kube-config
            key: path
    volumeMounts:
    - name: config
      mountPath: /etc/my-kube-config
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  volumes:
  - name: config
    configMap:
      name: kube-config
      items:
      - key: admin.conf
        path: admin.conf
```








