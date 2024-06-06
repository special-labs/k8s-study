## ch06 연습문제
- Deployment를 사용해 파드를 생성하고, ReplicaSet을 조정해 스케일링을 해본다.
- DaemonSet을 통해 파드를 생성해본다.
- 같은 Label을 가지면 두 컨트롤러가 담당하는 Pod가 어떻게 변경되는지 확인해본다.
----

### 1. Deployment를 사용해 파드를 생성하고, ReplicaSet을 조정해 스케일링을 해본다.
1. 아래 명시된 yaml을 통해 애플리케이션을 배포한다.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: numbers-web
  labels:
    study: ch06-dgr
spec:
  replicas: 1
  selector:
    matchLabels:
      lab: dgr-lab
  template:
    metadata:
      labels:
        lab: dgr-lab
    spec:
      containers:
        - name: web
          image: kiamol/ch03-numbers-web
```

2. `kubectl scale` 명령 또는 yaml 파일 업데이트를 통해 ReplicaSet을 3개로 조정한다.
```shell
kubectl scale deployment numbers-web --replicas=3
```

3. 새로 생성된 파드의 라벨이 기존 파드와 동일한지 확인한다.
```
kubectl get pods --show-labels
```

4. 동일한 라벨을 지정한 DaemonSet을 작성하고 적용한다.
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: numbers-web
  labels:
    study: ch06-dgr
spec:
  selector:
    matchLabels:
      lab: dgr-lab
  template:
    metadata:
      labels:
        lab: dgr-lab
    spec:
      containers:
        - name: web
          image: kiamol/ch03-numbers-web
```
    
5. cascade=orphan 옵션을 사용해 Daemonset을 삭제하고, Pod를 확인한다. (false 옵션은 deprecated)
```shell
kubectl delete ds numbers-web --cascade=orphan
kubectl get pods
kubectl get ds
```
6. Deployment의 replicas를 5로 올렸을 때, orphan pod가 이용되는지 확인해라.
```shell
kubectl scale deployment numbers-web --replicas=5
kubectl get pods
```

7. 삭제했던 DaemonSet 매니페스트를 다시 적용하고 orphan pod가 이용되는지 확인해라.


----
### 정리
- delete --cascade=orphan 옵션을 사용하면, 컨트롤러가 삭제되어도 Pod가 삭제되지 않는다.
- orphan pod는 차후 같은 스펙의 컨트롤러가 배포될 때 이용된다.
- 같은 label을 지정한 DaemonSet, Deployment 의 Pod라도 스케일링 시 근본?이 다른 orphan pod를 자신의 replicaSet에 포함시키지 않는다.