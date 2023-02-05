### ClusterIP

- selector의 label가 동일한 파드들의 그룹으로 묶어
- 단일 진입점 (Virtual-lP)을 생성
- 클러스터 내부에서만 사용가능
- type 생략 시 default 값으로 10.96.0.0/12 범위에서 할당됨

```yaml
# clusterip-nginx.yaml

apiVersion: v1
kind: Service
metadata:
  name: clusterip-service
spec:
  type: ClusterIP
  selector:
    app: webui
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
```


```yaml
# deploy-nginx.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: webui
spec:
  replicas: 3
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