# запускаем valve демон в кубере

Данный документ описывает то как удалось это сделать.

## сборка образа
- Dockerfile:
```
FROM registry.yandex.net/ubuntu:bionic

RUN apt-get update;\
    apt-get upgrade -y;\ 
    apt-get install repo-noc-bionic repo-noc-stable make cvs m4 python3-psycopg2 python3-requests python3-dateutil -y;\ 
    apt-get update

COPY ./root.crt /usr/local/share/ca-certificates/root.crt
COPY ./root.crt /root/.postgresql/root.crt
RUN update-ca-certificates

RUN apt-get install valve -y
ENTRYPOINT ["/usr/bin/valve", "--config=/valve-conf/valve.yaml"]
```
root.crt это сертификат для постгри, берем из салта или с тачки
- сделал репу, пушил вот так:
```
sudo docker build . -t registry.yandex.net/nocdev/valve
sudo docker push . -t registry.yandex.net/nocdev/valve
```

## конфиги для кубера демон части.
- valve-deployment.yaml:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: valve
spec:
  replicas: 2
  selector:
    matchLabels:
      app: valve
  template:
    metadata:
      labels:
        app: valve
    spec:
      serviceAccountName: sa
      containers:
        - name: valve
          image: registry.yandex.net/nocdev/valve
          imagePullPolicy: Always
          volumeMounts:
            - name: valve-conf
              mountPath: /valve-conf
              readOnly: true
            - name: valve-key
              mountPath: /valve-key
              readOnly: true
            - name: valve-cert
              mountPath: /valve-cert
              readOnly: true
          envFrom:
            - secretRef:
                name: env
      volumes:
        - name: valve-conf
          secret:
            secretName: valve-conf
        - name: valve-key
          secret:
            secretName: valve-key
        - name: valve-cert
          secret:
            secretName: valve-cert

      restartPolicy: Always
```
- подпихиваем в файлики cert.valve.yandex.net.pem, key.valve.yandex.net.pem, valve.yaml, env.yaml данные с тестовой тачки или салта, сотвественно сертификаты из nginx и конфиги valve, не забывем поменять пути в конфиге valve на то что было в valve-deployment.yaml.
- для nginx генерим отдельный tls секрет с key и crt вместе:
```
kubectl create secret tls nginx-cert --key key.valve.yandex.net.pem --cert cert.valve.yandex.net.pem 
```
- env файлик делаем вот так:
```
apiVersion: v1
kind: Secret
metadata:
  name: env
type: Opaque
data:
  AWS_ACCESS_KEY_ID: 
  AWS_SECRET_ACCESS_KEY: 
  GODEBUG:
  GOGC:
```
в переменные подпихиваем то что было в env на тачке, но пропущенное через base64
- деплой:
```
kubectl create secret generic valve-cert --from-file=./cert.valve.yandex.net.pem
kubectl create secret generic valve-key --from-file=./key.valve.yandex.net.pem
kubectl create secret generic valve-conf --from-file=./valve.yaml
kubectl apply -f env.yaml
kubectl apply -f valve-deployment.yaml
```
- смотрим в морду валва и в `kubectl get all -o wide`.

## статику в s3.
- делаем бакет в s3 и пушим туда статику, например получили `https://s3.mds.yanex.net/valve-test/manage.valve.yandex.net`

## nginx ingress конфиг
- с демоном все понятно, надо просто сделать сервис 'valve' и сделать в него proxy_pass.
- c мордой сложнее, надо сделать proxy_pass в s3. Для этого придется сделать сервис с типом ExternalName и указывать его.
Есть проблема с тем что ExternalName криво резолвит в v4, мне пришлось для POC сделать отдельную днс запись с ipv6 only.
у меня получилось вот так:
```
apiVersion: v1
kind: Service
metadata:
  name: valve
  labels:
    app: valve
spec:
  type: ClusterIP
  ports:
    - port: 14080
  selector:
    app: valve
---
apiVersion: networking.k8s.io/v1
kind: Service
apiVersion: v1
metadata:
  name: s3
spec:
  type: ExternalName
  externalName: s3.net.yandex.net
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: valve-ui
  annotations:
    nginx.ingress.kubernetes.io/upstream-vhost: "s3.mds.yandex.net"
    nginx.ingress.kubernetes.io/server-snippet: |
      proxy_intercept_errors on;
      error_page 404 =200 @error_pages;
      location @error_pages {
        proxy_set_header Host "s3.mds.yandex.net";
        rewrite .* "/valve-test/manage.valve.yandex.net/index.html" break;
        proxy_pass http://s3.net.yandex.net;
      }
    nginx.ingress.kubernetes.io/configuration-snippet: |
      rewrite /api/v(.*) /api/v$1 break;
      rewrite ^/$ /valve-test/manage.valve.yandex.net/index.html break;
      rewrite ^/(.*)$ /valve-test/manage.valve.yandex.net/$1 break;
spec:
  tls:
  - hosts:
    - k8s.valve.yandex.net
    secretName: nginx-cert
  rules:
  - host: k8s.valve.yandex.net
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: s3
            port:
              number: 80
      - path: /api/v1/
        pathType: Prefix
        backend:
          service:
            name: valve
            port:
              number: 14080
      - path: /api/v2/
        pathType: Prefix
        backend:
          service:
            name: valve
            port:
              number: 14080
  ingressClassName: nginx
```
почему все так сложно:
- нельзя сделать rewrite-target для одного path, кубер заставляет нас хостить морду и апи на разных доменах.
- морда работает так что вместо 404 надо отдавать index.html, локально с try_files все просто, но тут не так.
- первый реврайт в snippet нужен только для того чтобы не реврайтить /api. Да, можно сделать negative regex во втором реврайте, но у меня сходу не получилось.

## Автор статьи

Борис Литвиненко - borislitv@yandex-team.ru
