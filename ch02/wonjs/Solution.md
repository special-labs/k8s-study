### 답안
1. pod.yaml을 이용하여 pod를 생성하고, 생성된 pod의 상태를 확인
```bash
$ kubectl apply -f pod.yaml
```
2. 로컬 컴퓨터의 4000포트를 pod의 80포트로 포워딩 후 웹브라우저에서 4000 포트로 접속하여 웹페이지가 정상적으로 뜨는지 확인
```bash
$ kubectl port-forward wonjs-ch02-example 4000:80
```
3. 호스팅되고 있는 html의 일시적인 변경이 필요하여 현재 디렉토리에 제공된 index.html으로 내용 변경 후 웹브라우저에서 변경된 내용 확인
```bash
$ kubectl cp index.html wonjs-ch02-example:/usr/share/nginx/html/index.html
```
4. 사용된 pod 삭제
```bash
$ kubectl delete -f pod.yaml
```