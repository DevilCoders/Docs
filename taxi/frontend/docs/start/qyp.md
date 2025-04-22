# Настройка dev окружения (ЫПЬ, qyp)

Часть сервисов разрабатываются только на удалённой машине. Ниже инструкция по созданию и настройке такой машины.

## Шаг 1: Заказываем инстанс в облаке

1. Заполняем форму [тут](https://vmctl-web.taxi.yandex-team.ru/vms), сверху кнопка **Новая виртуалка**
2. В качестве имени, указываем свой ник. Образ - xenial. Датацентр - Сасово. Сеть `__TAXIDEVNETS__`
3. Ждём письмо о готовности виртуалки. Посмотреть доп. информацию можно можно [здесь](https://qyp.yandex-team.ru)
4. Пробуем подключиться `ssh {your login}@{your login}.sas.yp-c.yandex.net`
5. В случае ошибки `Permission denied (publickey)` ждём пока раскатится ключ на машинку(<= 2часа)

## Шаг 2: Настройка машинки

1. Заходим на машинку 
2. Просим админов добавить виртуалку в кондукторную группу *taxi_dev_front*. Можно попросить в чате [taxi-ito-helpline](https://t.me/joinchat/CbkpQEP-opKvYXFyFzevSQ). Тогда виртуалка получит все сетевые доступы от группы
3. Выполняем `sudo apt-get update` (не делайте `upgrade`).
4. Устанавливаем nodejs через [nvm](https://github.com/nvm-sh/nvm)
5. Создаём `.npmrc` файл
```bash
echo "registry=http://npm.yandex-team.ru" > ~/.npmrc &&\
sudo cp ~/.npmrc /root/
```

## Шаг 3: Заказ доменов

Заказать домен можно либо через службу экплуатации, либо при помощи dns-monkey.

### Через эксплуатацию

Пишем письмо на taxi-admin@yandex-team.ru

{% cut "Тело письма" %}

   `Тема`: Прописать DNS для моего дев окружения в ыпь
   `Текст`: Прошу прописать следующие dns записи## (список хостов - ваш инстанс)
   ```
   {user}.front.taxi.dev.yandex.ru -> {user}.sas.yp-c.yandex.net
   *.{user}.front.taxi.dev.yandex.ru -> {user}.sas.yp-c.yandex.net
   {user}.front.taxi.dev.yandex.com -> {user}.sas.yp-c.yandex.net
   *.{user}.front.taxi.dev.yandex.com -> {user}.sas.yp-c.yandex.net
   {user}.front.taxi.dev.yandex-team.ru -> {user}.sas.yp-c.yandex.net
   *.{user}.front.taxi.dev.yandex-team.ru -> {user}.sas.yp-c.yandex.net
   {user}.front.taxi.dev.yandex-team.net -> {user}.sas.yp-c.yandex.net
   *.{user}.front.taxi.dev.yandex-team.net -> {user}.sas.yp-c.yandex.net
   ```

{% endcut %}

[Пример задачи, которая создастся](https://st.yandex-team.ru/TAXIADMIN-11524)

### Через dns-monkey

{% note info %}

Выполняем на сервере

{% endnote %}

Установите [dns-monkey](https://wiki.yandex-team.ru/dynamic-dns/dns-monkey-roadmap/).

Сохраните информацию о вашем FQDN и логине через переменные окружения:

```bash
DNS_ACTION=add DEV_USERNAME=$USER DEV_FQDN={your login}.sas.yp-c.yandex.net
```

Запустите скрипт

```bash
dns-monkey.pl --zone-update --expression "$DNS_ACTION-cname $DEV_USERNAME.front.taxi.dev.yandex.ru $DEV_FQDN" &&\
dns-monkey.pl --zone-update --expression "$DNS_ACTION-cname *.$DEV_USERNAME.front.taxi.dev.yandex.ru $DEV_FQDN" &&\
dns-monkey.pl --zone-update --expression "$DNS_ACTION-cname $DEV_USERNAME.front.taxi.dev.yandex.com $DEV_FQDN" &&\
dns-monkey.pl --zone-update --expression "$DNS_ACTION-cname *.$DEV_USERNAME.front.taxi.dev.yandex.com $DEV_FQDN" &&\
dns-monkey.pl --zone-update --expression "$DNS_ACTION-cname $DEV_USERNAME.front.taxi.dev.yandex.net $DEV_FQDN" &&\
dns-monkey.pl --zone-update --expression "$DNS_ACTION-cname *.$DEV_USERNAME.front.taxi.dev.yandex.net $DEV_FQDN" &&\
dns-monkey.pl --zone-update --expression "$DNS_ACTION-cname $DEV_USERNAME.front.taxi.dev.yandex-team.ru $DEV_FQDN" &&\
dns-monkey.pl --zone-update --expression "$DNS_ACTION-cname *.$DEV_USERNAME.front.taxi.dev.yandex-team.ru $DEV_FQDN"
```

Обновление DNS-записей занимает определенное время, но вы можете продолжать настраивать сервер, не дожидаясь их.
После вы сможете подключиться к виртуалке по любому из доменов, где `DEV_USERNAME` — то, что было передано в команде выше:

```
$DEV_USERNAME.front.taxi.dev.yandex.ru
$DEV_USERNAME.front.taxi.dev.yandex.com
$DEV_USERNAME.front.taxi.dev.yandex.net
$DEV_USERNAME.front.taxi.dev.yandex-team.ru
```

После запуска скрипта могут сыпаться ошибки типа `Error: serivce is not accessible`, скорее всего не хватает ролей, обратитесь за помощью к руководителю или команде.

Если нужно удалить записи, то следует указать `DNS_ACTION=delete`. Это может потребоваться во время учений, чтобы перенаправить запросы на тачку в другом дц.

{% cut "Если забыли/потеряли FQDN, указанный при добавлении записи" %}

Можно погрепать по существующим записям и узнать FQDN, выполнив, где `$DEV_USERNAME` — логин, который был указан при создании записи

```bash
dns-client --zone-content --zone "front.taxi.dev.yandex-team.ru" | grep $DEV_USERNAME
dns-client --zone-content --zone "front.taxi.dev.yandex.ru" | grep $DEV_USERNAME
dns-client --zone-content --zone "front.taxi.dev.yandex.com" | grep $DEV_USERNAME
dns-client --zone-content --zone "front.taxi.dev.yandex.net" | grep $DEV_USERNAME
```

Затем можно воспользоваться командой для удаления, указанной выше

{% endcut %}

## Шаг 4: Заказ сертификата

1. Запросите внутренний сертификат в [Сертификаторе](https://crt.yandex-team.ru/certificates). Подробней [тут](https://wiki.yandex-team.ru/geo-admin/https_for_dev_server/#1.zakazsertifikata).
   
Данные для заказа:

```
   CA name: %%InternalCA%%
   АBC-сервис: https://abc.yandex-team.ru/services/taxi/
   Хосты: {your login}.front.taxi.dev.yandex.net, *.{your login}.front.taxi.dev.yandex.net, {your login}.front.taxi.dev.yandex.ru, *.{your login}.front.taxi.dev.yandex.ru, {your login}.front.taxi.dev.yandex.com, *.{your login}.front.taxi.dev.yandex.com, {your login}.front.taxi.dev.yandex-team.ru, *.{your login}.front.taxi.dev.yandex-team.ru
```
   
2. Скачайте `.pem` сертификат и положите на вашу машинку в `/etc/ssl/yandex/server.pem`, выдайте прав файлу. [Подробней](https://wiki.yandex-team.ru/geo-admin/https_for_dev_server/#3.kopirovaniesertifikata)

## Шаг 5: Настройка nginx

{% note info %}

Выполняем на сервере

{% endnote %}

1. Указываем сертификат полученный выше
```bash
sudo mkdir /etc/nginx/conf.d &&\
sudo touch /etc/nginx/conf.d/01-ssl.conf &&\
echo "\
listen [::]:443 ssl;

ssl_certificate /etc/ssl/yandex/server.pem;
ssl_certificate_key /etc/ssl/yandex/server.pem;

ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_ciphers kEECDH+AESGCM+AES128:kEECDH+AES128:kRSA+AESGCM+AES128:kRSA+AES128:DES-CBC3-SHA:!RC4:!aNULL:!eNULL:!MD5:!EXPORT:!LOW:!SEED:!CAMELLIA:!IDEA:!PSK:!SRP:!SSLv2;
ssl_session_cache shared:SSL:128m;
ssl_session_timeout 28h;
" | sudo tee /etc/nginx/conf.d/01-ssl.conf
```

2. Проверяем работу nginx `sudo nginx -t`
3. Если всё хорошо - рестартим `sudo service nginx restart`
