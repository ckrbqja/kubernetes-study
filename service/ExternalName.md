### ExternalName

- 클러스터 내부에서 External의 도메인 생성

```yaml
apiVersion: v1
kind: Service
metadata:
  name: externalname-svc
spec:
  type: ExternalName
  externalName: google.com
```