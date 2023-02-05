
### StatefulSet
- Pod의 상태를 유지
  - Pod 이름
  - Pod의 볼륨

```shell
$ kubectl create -f statefulset-exam.yaml
# Pod가 생성되는 이름과 생성되는 과정을 확인해보자.

$ kubectl get statefulsets,pod

# 동작중인 두 번해 pod를 삭제하면 어떤 일이 일어나나?
$ kubectl delete pod sf-nginx-1

# scale down or up
어떤 순서로 확장 및 축소되는가?
$ kubectl scale statefulset sf-nginx --replicas=2
$ kubectl scale statefulset sf-nginx --replicas=4

# rolling update && rollback
$ kubectl edit statefulsets.apps sf-nginx
$ kubectl rollout undo statefulsets.apps sf-nginx
```

> edit 할 시 default 롤링업데이트