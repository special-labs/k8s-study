## ch05 연습문제
### 교재 연습문제로 대체한다

----

- ch05/lab/todo-list 디렉터리 내 매니페스트를 `kubectl apply` 명령을 통해 배치하라.
  - 해당 매니페스트에는 proxy 서비스, webApp 용 deployment가 포함되어 있다.


- 로드밸런서 리소스를 가리키는 URL을 찾아 브라우저 내에서 애플리케이션에 접근해라.
  - 응답하지 않는다면, 로그를 확인하여 문제점을 찾고 해결하라.


- 프록시의 캐시와 웹 앱 파드의 DB 파일을 둘 `Persistence Volume`을 생성해라.
  - 파드의 정의와 로그를 보고 마운트 대상이 어디인지 알아내야 한다.


- 애플리케이션이 정상 동작한다면 할 일 항목을 몇개 추가하고, 모든 파드를 삭제해라.
  - 삭제 이후 페이지를 새로고침한 후에도 데이터가 그대로 유지되어 있어야 한다.


- 볼륨 유형과 스토리지 유형은 제한 없이 사용할 수 있다. 실습 혼경해서 어떤 것을 사용할 수 있는지 확인해 보아라.