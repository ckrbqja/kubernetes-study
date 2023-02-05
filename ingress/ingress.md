### ingress
  - HTTP나 HTTPS를 통해 클러스터 내부의 서비스를 외부로 노출
  - 기능
    - Service에 외부 URL을 제공
    - 트래픽을 로드밸런싱
    - SSL 인증서 서리
    - Virtual hosting을 지정

https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters
```shell
# Bare metal clusters
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.5.1/deploy/static/provider/baremetal/deploy.yaml
```


lngress를 이용한 웹서비스 운영: namespace 치환 
- Default namespace 치환 : kubectl config
# kubectl config —help
# kubectl config view
# kubectl config set-context ingress-admin@kubernetes --cluster=kubernetes --user=kubernetes-admin --namespace=ingress-nginx
# kubectl config view
# kubectl config use-context ingress-admin@kubernetes
# kubectl config current-context
# kubectl get all
# kubectl apply -f marvel-home.yaml -f pav.yaml

```yaml
# ingress rule
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: marvel-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: marvel-service
                port:
                  number: 80
          - path: /pay
            pathType: Prefix
            backend:
              service:
                name: marvel-service
                port:
                  number: 80
```


```yaml
# marvel-home.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: marvel-home
spec:
  selector:
    matchLabels:
      name: marvel
  template:
    metadata:
      labels:
        name: marvel
    spec:
      containers:
        - name: marvel-controller
          image: smlinux/marvel-collection
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: marvel-service
spec:
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
  selector:
    name: marvel

```

```yaml
# pay.yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: pay-rc
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: pay
    spec:
      containers:
        - name: pay
          image: smlinux/pay
          ports:
            - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: pay-service
spec:
  ports:
    - port: 80
      targetPort: 8080
  selector:
    app: pay
```