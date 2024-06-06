## ch04 연습문제
- deployment를 생성하고, configmap을 사용하여 파드의 환경변수를 설정해본다.
- volumeMounts를 사용하여 파드의 교체 없이 실행중인 애플리케이션의 설정을 변경해본다.
----

### 1. ConfigMap을 사용한 환경변수 설정
1. 환경변수를 담을 `ch04-practice.env` 파일을 생성하고, 다음 내용을 추가한다.
    ```properties
    APP_NAME=ch04-practice
    APP_VERSION=1.0
    ```

2. `ch04-practice.env` 파일을 참조하는 `ch04-configmap`을 생성한다.
    - 만들어진 configmap을 kubectl 커맨드를 통해 yaml 파일로 저장한다.
    ```
    kubectl create configmap ch04-configmap --from-env-file=ch04-practice.env
    kubectl get configmap ch04-configmap -o yaml > ch04-configmap.yaml
    ```

3. `ch04-configmap`을 사용하는 Deployment를 작성한다. 파드는 `busybox` 이미지를 사용한다.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
   name: ch04-practice
spec:
   selector:
      matchLabels:
         app: ch04-practice
   template:
      metadata:
         labels:
            app: ch04-practice
      spec:
         containers:
            - name: ch04-practice
              image: busybox
              command: ['sh', '-c', 'while true; do echo The app color is $APP_NAME and version is $APP_VERSION; sleep 2; done']
              env:
                 - name: APP_NAME
                   valueFrom:
                      configMapKeyRef:
                         name: ch04-configmap
                         key: APP_NAME
                 - name: APP_VERSION
                   valueFrom:
                      configMapKeyRef:
                         name: ch04-configmap
                         key: APP_VERSION

``` 

4. ConfigMap을 적용하고, 작성한 Deployment를 배포한다. 이후 파드가 정상적으로 생성되었는지 확인한다.
    ```
    kubectl apply -f ch04-configmap.yaml
    kubectl apply -f ch04-deployment.yaml
    kubectl get pod -l app=ch04-practice
    ```
5. 파드의 로그를 확인한다.
    ```
    kubectl logs -f ch04-practice-xxxxx
    ```

6. ConfigMap 내 APP_VERSION 내용을 변경하고, 파드의 로그를 확인한다.
    ```
    kubectl edit configmap ch04-configmap
    kubectl logs -f ch04-practice-xxxxx
    ```

7. 파드 로그의 환경변수가 바뀌는지 확인한다.

----
### 2. 동적 환경변수 적용
8.  작성한 Deployment에 volumeMounts를 적용하여, 파드의 환경변수를 동적으로 변경해본다.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ch04-practice
spec:
  selector:
    matchLabels:
      app: ch04-practice
  template:
    metadata:
      labels:
        app: ch04-practice
    spec:
      containers:
        - name: ch04-practice
          image: busybox
          command: ['sh', '-c', 'while true; do echo The app name is $(cat /app/config/app-name) and version is $(cat /app/config/app-version); sleep 2; done']
          volumeMounts:
            - name: config
              mountPath: "/app/config"
              readOnly: true
      volumes:
        - name: config
          configMap:
            name: ch04-configmap
            items:
              - key: APP_NAME
                path: app-name
              - key: APP_VERSION
                path: app-version
```

9. Deployment를 업데이트하고, 파드의 로그를 확인한다.
    ```
    kubectl apply -f ch04-deployment.yaml
    kubectl get pod -l app=ch04-practice
    kubectl logs -f ch04-practice-xxxxx
    ```
10. ConfigMap 내 APP_VERSION 내용을 변경하고, 파드의 로그를 확인한다.
    ```
    kubectl edit configmap ch04-configmap
    kubectl logs -f ch04-practice-xxxxx
    ```

11. 파드가 교체되는지, 그리고 파드 로그의 환경변수가 바뀌는지 확인한다.