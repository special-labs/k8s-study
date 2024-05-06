### 연습문제

1. Deployment 작성 
   - pod.yaml에 사용된 이미지를 사용하라.
   - 임의의 label을 추가하라.
   - replicas는 3개로 설정.
   - containerPort는 8090으로 설정.


2. 작성된 Deployment를 통해 Pod를 생성하라. 


3. deloyment에 정의한 `label`로 pod를 조회하라. (replicas가 3개인지 확인)


4. `scale` 명령어를 통해 replicas를 2개로 줄여라.


5. Deployment의 상태 및 스펙을 확인하고, `edit` 명령어를 통해 containerPort를 80으로 수정하라.


6. 수정된 pod가 배포된 이후, local 8088 -> 80 으로 `port-forward` 명령을 통해 바인딩 후 접속하라.


7. deployment를 삭제하라.
