### 연습문제
pod.yaml에 정의되어 있는 컨테이너는 nginx를 통해서 웹페이지를 호스팅하고 있음 (기본 포트 80)
1. pod.yaml을 이용하여 pod를 생성하고, 생성된 pod의 상태를 확인
2. 웹브라우저에서 4000 포트로 접속하여 웹페이지가 정상적으로 뜨는지 확인
3. 호스팅되고 있는 html을 일시적으로 변경이 필요하여 현재 디렉토리에 제공된 index.html으로 내용 변경
4. 웹브라이저에서 4000 포트로 접속하여 변경된 내용 확인
5. 사용된 pod 삭제
<br>

컨테이너 내부 index.html 파일 경로
```
/usr/share/nginx/html/index.html
```