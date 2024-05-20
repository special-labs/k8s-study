## 문제: ConfigMap 및 Secret을 사용한 애플리케이션 설정

새로운 애플리케이션을 배포하는 과정에서 설정 정보와 비밀 정보를 안전하게 관리하기 위해 ConfigMap과 Secret을 사용하여 애플리케이션의 환경 변수를 설정하고, 비밀 정보를 주입해야 한다.

### 문제 1. 다음과 같은 설정 정보를 포함하는 ConfigMap을 작성하세요
- 이름: config
- 설정 항목:
    - APP_ENV: production
    - APP_DEBUG: false

### 문제 2. 다음과 같은 비밀 정보를 포함하는 Secret을 만드는 명령어를 작성하세요
- 이름: secret
- 비밀 항목:
    - DB_USERNAME: admin
    - DB_PASSWORD: s3cr3t

### 문제 3. 위에서 생성한 ConfigMap과 Secret을 사용하는 Deployment를 작성하세요
- 이름: app
- replica 수: 1
- container 이름: container
- image: nginx:latest
- 환경 변수:
    - APP_ENV는 config의 APP_ENV 값을 사용
    - APP_DEBUG는 config의 APP_DEBUG 값을 사용
    - DB_USERNAME는 secret의 DB_USERNAME 값을 사용
    - DB_PASSWORD는 secret의 DB_PASSWORD 값을 사용



