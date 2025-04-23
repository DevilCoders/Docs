# Redeploy cockroach node
Порядок дествий при переналивке/восстановлении ноды cockroachdb.

1. Собираем на Linux машинке https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/bootstrap/cockroach

2. Идем на живую ноду кластера (sas, vla, man, msk, prestable) и создаем там нужную структура каталогов для выполнения настройки ноды и приносим туда собранные скрипты:

        mkdir cockroach
        cd cockroach
        mkdir certs nodes my-safe-directory
        scp -r <your-node>:'<path-to-infra/hmserver/bootstrap/cockroach>/*' .

3. Приносим закрытый ключ для соответствующего кластера из секретницы https://yav.yandex-team.ru/secret/sec-01efy99nzq5n09n2bnq0pb599t/explore/versions :

        vim my-safe-directory/ca.key

4. Приносим его ca.crt:

        cp /var/lib/cockroach/certs/ca.crt certs

5. Генерируем сертификаты для ноды с fqdn:

        ./scripts/create-node.sh <fqdn>

6. Генерируем клиентские сертификаты:

        ./scripts/create-client-certs.sh root

7. Запускаем бинарь деплоя ноды:

        ./cmd/cockroach-bootstrap --path configs/<cluster>.yaml redeploy-node --node <fqdn> --certs nodes/<fqdn>

8. Смотрим на результат в вебморде cockroach по адресу https://<known-node>:8888 (логин/пароль можно взять в той же секретнице, что и ключи), нода должна успешно добавиться в кластер.

9. После того, как все underreplicated sequences ушли в ноль, смотрим айдишник старой ноды с этим же fqdn:

        sudo cockroach node --host <fqdn> --certs-dir /var/lib/cockroach/certs status

10. Убиваем нерабочу ноду:

        sudo cockroach node --host <fqdn> --certs-dir /var/lib/cockroach/certs decommission <old-id>

11. Наблюдаем живой и здоровый кластер.

*Не забываем, что cockroach живет вместе с hm-server, а ему после переналивки нужно подложить файлик /etc/hm-server-env.conf*

*Также нужно поднять hm-reporter*
1. Подкладываем пароль из https://yav.yandex-team.ru/secret/sec-01efy99nzq5n09n2bnq0pb599t/explore/versions в [hm-reporter-server.conf](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/bootstrap/hm-reporter/templates/hm-reporter-server.conf)
2. Запускаем `./cmd/hm-reporter-bootstrap <fqdn>`

*Если при переналивке ноды была смена ip аддрессов, не забываем перебить ip бэкендов в awacs*
* [prestable](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hm-server-prestable/backends/list/hm-reporter/show/)
* [sas](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hm-server-sas/backends/list/hm-reporter/show/)
* [vla](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hm-server-vla/backends/list/hm-reporter/show/)
* [man](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hm-server-man/backends/list/hm-reporter/show/)
* [msk](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hm-server-msk/backends/list/hm-reporter/show/)