### LoadBalancer.md

- Public 클라우드(AWS, Azure, GCP)에서 운영가능
- LoadBalancer를 자동으로 구성 요청
- NodePort를 예약 후 해당 nodeport로 외부 접근 허용

```yaml
apiVersion: v1
kind: Service
metadata:
  name: loadbalancer-service
spec:
  type: LoadBalancer
  selector:
    app: webui
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
```

