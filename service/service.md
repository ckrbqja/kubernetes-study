### Kubernetes Service

- 동일한 서비스를 제공하는 Pod그룹의 단일 진입점을 제공

- type 종류
  - ClusterIP
  - NodePort
  - LoadBalancer
  - ExternalName
  
```yaml
apiVersion: v1
kind: Service
metadata:
  name: webui-svc
spec:
  clusterIP: 10.96.100.100
  selector:
    app: webui
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
      
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webui
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