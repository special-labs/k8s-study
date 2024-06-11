## ch06 연습문제
- 실습환경이 단일 노드임을 가정한다.

### 1. sample/nginx.yaml을 실행 해본다 
아래 명령어를 실행하면 proxy pod를 유지하는 데몬셋이 생성된다.
```shell
kubectl apply -f sample/nginx.yaml
```

### 2. sample/nginx.yaml을 보고 문제 해결
1. 아래 명령을 실행시 proxy pod가 나오지 않은 이유를 설명하시오. (만약 나온다면 나오는 이유를 설명하시오)
```shell
kubectl get pods 
```
2. 명시된 yaml파일에 의하여 데몬셋이 정상적으로 실행될 수 있도록 설정한다. (노드의 label 변경)
```shell
kubectl label node $(kubectl get nodes -o jsonpath='{.items[0].metadata.name}') study=nginx --overwrite
```

### 3. 기존의 로직은 정상적으로 동작하길 원하고 데몬셋을 삭제하고 싶을 경우 사용할 수 있는 명령어를 작성
```shell
kubectl delete ds proxy --cascade=orphan
```