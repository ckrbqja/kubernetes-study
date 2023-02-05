### Headless

- ClusterIP가 없는 서비스로 단일 진입점이 필요 없을 때
- Service와 연결된 Pod의 endpoint로 DNS레코드가 생성
- Pod의 DNS주소: [pod-ip-addr].[namespace].pod.cluster.local

```yaml
# headless-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: headless-service
spec:
  type: ClusterIP
  clusterIP: None #<<headless
  selector:
    app: webui
  ports:
    - port: 80
```

```shell

NAME                         READY   STATUS    RESTARTS   AGE   IP              NODE        NOMINATED NODE   READINE
SS GATES
pod/webui-6d4c4cc4b8-bvmcf   1/1     Running   0          35m   20.109.131.14   k8s-node2   <none>           <none>
pod/webui-6d4c4cc4b8-d2spw   1/1     Running   0          35m   20.111.156.77   k8s-node1   <none>           <none>
pod/webui-6d4c4cc4b8-mfbq6   1/1     Running   0          35m   20.111.156.78   k8s-node1   <none>           <none>


curl 20-109-131-14.default.pod.cluster.local
```