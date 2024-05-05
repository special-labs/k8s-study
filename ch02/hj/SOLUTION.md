```bash
$ kubectl apply -f deployment.yaml
```
```bash
$ kubectl logs --tail=5 POD_NAME
```
```bash
$ docker container logs --tail=5 CONTAINER
```
```bash
$ kubectl delete -f deployment.yaml
```

### kubectl logs
- 쿠버네티스 클러스터 내의 특정 파드의 로그를 확인
- 해당 파드의 로그를 볼 수 있는 쿠버네티스 권한이 필요
### docker container logs
- 로컬 머신 또는 특정 도커 호스트에 있는 도커 컨테이너의 로그를 확인
- 도커 데몬에 액세스할 수 있는 권한이 필요
