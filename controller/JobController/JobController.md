```shell
[root@k8s-master stateful]# kubectl run testpod --image=centos:7 --command sleep 5
```

### Job
- k8s는 pod를 running 중인 상태로 유지
- Batch 처리 pod는 작업이 완료되면 종료됨
- Batch 처리에 적합한 컨트롤러로 pod의 성공적인 완료를 보장
  - 비정상 종료시 다시실행
  - 정상 종료시 완료

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: job-example
spec:
  template:
    spec:
      containers:
        - name: centos-container
          image: centos:7
          command: ["bash"]
          args:
            - "-c"
            - "echo 'Hello World'; sleep 50; echo 'Bye'"
      restartPolicy: Never
      #restartPolicy: OnFailure
  #backoffLimit: 3
```