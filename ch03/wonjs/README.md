## 연습문제
### 문제1
클러스터에 mario, 2048 2개의 파드가 실행 중일 때 하나의 yaml을 작성하여 두 파드 모두 외부에서 접근이 가능하도록 서비스를 생성하라
- 외부 연결 포트는 자유롭게 설정
- mario application은 8080를 사용하고, 2048 application은 80을 사용하고 있음
### 문제2
(심화 문제 - 필수 아니고 생각해보기) <br>
http://localhost:8080/mario 는 mario 게임으로, http://localhost:8080/2048 는 2048 게임으로 접근하도록 서비스를 생성하라