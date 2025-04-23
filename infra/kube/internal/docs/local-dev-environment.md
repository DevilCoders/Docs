[minikube](https://minikube.sigs.k8s.io/docs/) — очень удобная штука для поднятия локальной инсталляции Kubernetes.

При разработке контроллеров CRD в Аркадии возникает нюанс:
* только что собранный с помощью ya make контроллер хочется запустить на «железном» хосте, а не внутри локального кластера — чтобы избежать шагов, связанный со сборкой Docker-образа, его заливкой в registry и выкладкой;
* как следствие, использование механизмов вроде [cert-manager](https://cert-manager.io/docs/), которые могут подсовывать выпущенные (в том числе и самоподписанные) сертификаты везде, где нужно, становится невозможным;
* общение API-сервера с веб-хуками, которые реализует наш контроллер, происходит исключительно по `https://`.

При этом «железный» хост изнутри minikube [доступен](https://minikube.sigs.k8s.io/docs/handbook/host-access/) по имени `host.minikube.internal`.

Идея заключается в том, чтобы завести самоподписанный рутовый сертификат и:
* [научить minikube ему доверять](https://minikube.sigs.k8s.io/docs/handbook/untrusted_certs);
* выпустить для нашего контроллера сертификат, самоподписанный нашим рутовым;
* в поле `clientConfig` конфигов [WebhookClientConfig](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#webhookclientconfig-v1-admissionregistration-k8s-io) наши веб-хуки адресовать по URL, а не через ссылку на `service`, подразумевающую, что реализация веб-хуков запущена в этом же кластере.

## Про сертификаты
Loosely based on https://wiki.yandex-team.ru/users/anton-k/ssl/client/.

### Как выпустить рутовый сертификат
Формируем сертификат CA:
```shell
openssl genrsa -aes256 -passout pass:xxxx -out ca.pass.key 4096
openssl rsa -passin pass:xxxx -in ca.pass.key -out ca.key
openssl req -new -x509 -days 3650 -key ca.key -out ca.pem
```

### Как заставить minikube ему доверять
```shell
cp ./ca.pem $HOME/.minikube/certs/kube-awacs-ctl.pem
```
Затем делаем `minikube stop` и `minikube start --embed-certs`, как то предписывает [документация](https://minikube.sigs.k8s.io/docs/handbook/untrusted_certs/#tutorial).

### Как выпустить самоподписанный сертификат для контроллера
Заметки:
* Golang версии 1.15 депрекейтит [использование CN (common name)](https://tip.golang.org/doc/go1.15#commonname), поэтому в сертификате обязательно должны быть указаны SAN (subject alternative names) — иначе API-сервер доверять им не будет;
* если какой-то из шагов на OS X фейлится с ошибкой вроде `routines:CRYPTO_internal:variable has no value`, стоит попробовать OpenSSL, поставленный через brew (обычно `export PATH="/usr/local/opt/openssl/bin:$PATH"`, см. https://stackoverflow.com/a/34612992).

Создаём файл `./openssl.cnf` c примерно следующим содержимым:
```
[ req ]
prompt = no
distinguished_name = req_distinguished_name
attributes = req_attributes

[ req_distinguished_name ]
commonName = ${ENV::SAN}

[ req_attributes ]

[ v3_req ]
basicConstraints = CA:FALSE
keyUsage = nonRepudiation, digitalSignature, keyEncipherment
extendedKeyUsage = clientAuth

[ san_env ]
subjectAltName = DNS:${ENV::SAN}
```

Создаём файл `./v3.ext` c примерно следующим содержимым:
```
basicConstraints = CA:FALSE
keyUsage = nonRepudiation, digitalSignature, keyEncipherment
extendedKeyUsage = clientAuth

[ san_env ]
subjectAltName = DNS:${ENV::SAN}
```

Создаём клиентский ключ:
```shell
openssl genrsa -aes256 -passout pass:xxxx -out client.pass.key 4096
openssl rsa -passin pass:xxxx -in client.pass.key -out tls.key
```

Создаём CSR (certificate signing request):
```shell
SAN="host.minikube.internal" openssl req -new -config ./openssl.cnf -key tls.key -out client.csr -extensions san_env
```

И делаем сам сертификат:
```shell
SAN="host.minikube.internal" openssl x509  -extensions san_env -req -days 3650 -in client.csr -CA ca.pem -CAkey ca.key -set_serial 01 -extfile v3.ext -out tls.crt
```

Voila! Файлы `./tls.crt` и `./tls.key` можно положить в отдельную директорию (и, например, указать её в качестве `certDir` в [опциях manager](https://pkg.go.dev/sigs.k8s.io/controller-runtime/pkg/manager#Options), если используется sigs.k8s.io/controller-runtime).

### Пример ValidatingWebhookConfiguration
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#validatingwebhook-v1-admissionregistration-k8s-io
```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingWebhookConfiguration
metadata:
    creationTimestamp: null
    name: validating-webhook-configuration
webhooks:
    - admissionReviewVersions:
          - v1
      clientConfig:
          url: https://host.minikube.internal:31337/validate-awacs-yandex-team-ru-v1-dnsrecord
      failurePolicy: Fail
      name: vdnsrecord.kb.io
      rules:
          - apiGroups:
                - awacs.yandex-team.ru
            apiVersions:
                - v1
            operations:
                - CREATE
                - UPDATE
            resources:
                - dnsrecords
      sideEffects: None
```
