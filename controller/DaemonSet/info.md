
### DaemonSet

- 전체 노드에서 Pod가 한 개씩 실행되도록 보장
- 로그 수입기나 모니터 에이전트 같은 프로그램에 적용

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: aaa
spec:
  selector:
    matchLabels:
      app: webui
  template:
    metadata:
      name: nginx-pod
      labels:
        app: webui
    spec:
      containers:
        - name: nginx-container
          image: nginx:1.14
```

>DaemonSet은 edit로 yaml변경 시 롤링 업데이트로 적용
<br>
```shell
#롤백
kubectl rollout undo daemonset [이름] 
```