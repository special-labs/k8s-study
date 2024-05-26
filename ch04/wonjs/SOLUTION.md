1. MYSQL_DATABASE 환경변수를 설정하는 configMap을 생성하라. (key: MYSQL_DATABASE, value: dior)
```bash
kubectl create configmap mysql-info --from-literal=MYSQL_DATABASE='dior'
```
2. MYSQL_ROOT_PASSWORD 환경변수를 설정하는 secret을 생성하라. (key: MYSQL_ROOT_PASSWORD, value: k8s_DB_password)
```bash
kubectl create secret generic mysql-secret --from-literal=MYSQL_ROOT_PASSWORD=k8s_DB_password
```
3. deployment.yaml을 사용하여 adminer와 mysql을 배포하라.
```bash
kubectl apply -f deployment.yaml
```
4. adminer에서 mysql에 접근할 수 있도록 service를 생성하라.
```bash
kubectl apply -f service.yaml
```
5. adminer 웹페이지에서 dior DB에 접속하라.(adminer 서버 입력칸에 mysql:3306으로 접속)