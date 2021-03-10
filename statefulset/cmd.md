# command

kubectl scale statefulset web --replicas=0

kubectl delete pvc www-web-2

kubectl delete pv pv1

# scanario 1

* scale replicas 3 -> 2
* 删除 pvc
* scale replicas 2 -> 3
* pod会使用一个新的pv
* 直到pv被删除(reclaim policy = retain)，才会被重新使用




