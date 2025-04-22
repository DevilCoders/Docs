# Заводим новый сервис

## 1. Домены
В принципе никаких ограничений, но нужно помнить что мы пилим в основном залогиновые сервисы и что это должны быть wildcard-домены на которые можно выписать сертификат в `InternalCA`.
Примеры:
  * `*.verstka-dev.mail.yandex.{ru,com,com.tr,co.il,....}`;
  * `*.magic-dev.mail.yandex-team.ru`;
  * `*.super-dev.dst.yandex.{ru,com,net}`.

Домены должны быть алиасами (`CNAME`) к балансеру `proxy-verstka-dev.mail.yandex.net`.

За заведением доменов в зонах `mail.yandex.TLD/mail.yandex-team.ru` обращаться к [Пете Бурмистрову](https://staff.yandex-team.ru/pierre).
Для других зон просите их ответственных или попробуйте через [DNS Manager](https://dns.tt.yandex-team.ru/request).

## 2. Сертификаты
Для всех доменов из п.1 нужно выписать один(!) сертификат в [Сертификатнице](https://crt.yandex-team.ru/certificates?cr-form=1). CA Name должен быть **InternalCA**.
Когда сертификат приедет в [Секретницу](https://yav.yandex-team.ru/) (вам придёт письмо), в нём нужно добавить доступ на чтение роботу **robot-mail-internal** и переименовать ключи из `SOMELONGRANDOMSTRING_{certificate,private_key}` в `certificate` и `private_key` соответственно.

## 3. Конфиг прокси (tools/docker-images/proxy-verstka-dev)
:warning: Ниже `SERVICE` замените на кодовое имя вашего сервиса (`sarah`, `tuning` и т.п.)

В папку [etc/nginx/sites-available](./docker-images/proxy-verstka-dev/etc/nginx/sites-available/) добавляем конфиг `SERVICE-dev.conf` по аналогии с `tuning-dev.conf` (простой). Более развесистый конфиг можно посмотреть в `verstka-dev.conf`.

В файл [etc/yandex/yav-deploy/defaults.conf](./docker-images/proxy-verstka-dev/etc/yandex/yav-deploy/defaults.conf) добавляем две строчки (`sec-01....` — ID секрета из п.2)
```
/SERVICE-dev.crt = sec-01....[certificate]
/SERVICE-dev.key = sec-01....[private_key]
```
В файл [service.sh](./docker-images/proxy-verstka-dev/service.sh) добавляем строчки
```
if [[ ! -f /secrets/nginx/SERVICE-dev.crt ]]; then
    echo "Failed to get certificates, cannot start"
    exit 1
fi
```

После аппрува можно собрать докер-образ
```
cd tools/docker-images/proxy-verstka-dev
make
```
отредактировать `tools/docker-images/proxy-verstka-dev/spec.yaml` (поменять [`tag`](https://github.yandex-team.ru/personal-services/frontend/blob/dev/tools/docker-images/proxy-verstka-dev/spec.yaml#L32)) и выкатить его в [Y.Deploy](https://yd.yandex-team.ru/stages/mail_proxy_verstka_dev).
```bash
make deploy
```
Изменения в `spec.yaml` закоммитить в репозиторий.

## 4. Конфиг QYP (tools/qyp)
:warning: Ниже `SERVICE` замените на кодовое имя вашего сервиса (`sarah`, `tuning` и т.п.)

Добавляем конфиг `SERVICE.conf` nginx в [плейбук sites-available](./qyp/roles/nginx/files/nginx/sites-available/) опять же по аналогии c `tuning.conf`.

Правим [main.yaml](./qyp/roles/nginx/tasks/main.yaml). Добавляем создание линка на конфиг и папки для логов. Поищите в файле слово `tuning` и добавьте аналогичную строчку рядом.
