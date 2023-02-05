### NodePort

- 모든 노드를 대상으로 외부 접속 가능한 포트를 예약
- Default NodePort 범위: 30000-32767
- ClusterIP를 생성 후 NodePort를 예약

```yaml
# nodeport-nginx.yaml
apiVersion: v1
kind: Service
metadata:
  name: nodeport-service
spec:
  type: NodePort
  clusterIP: 10.100.100.200
  selector:
    app: webui
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
      nodePort: 30200
```