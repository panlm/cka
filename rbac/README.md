## reference

`https://kubernetes.io/zh/docs/reference/access-authn-authz/rbac/`

## create sa

```
kubectl create sa sa1
```

## create role

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""] # "" 标明 core API 组
  resources: ["services","pods"]
  verbs: ["get", "watch", "list"]
```

## create rolebinding

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-reader
  namespace: default
subjects:
- kind: ServiceAccount
  name: sa1
  namespace: default
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

## run as service account

```sh
# could access
kubectl get po --as=system:serviceaccount:default:sa1
# could NOT access
kubectl logs pod/pod_name --as=system:serviceaccount:default:sa1
```






