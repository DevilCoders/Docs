# Разворачиваем dev-стенд

## Разворачиваем consul-сервера

Начинаем с `consul-common`:

Плейбуки:
* [vertis_vdev_consul_common](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vdev_consul_common.yml)
* [vertis_vdev_consul_server](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vdev_consul_server.yml)

1. Наливаем необходимое количество хостов через `terraform`. Сразу же после наливки хоста необходимо отключить ansible-pull (`vertis-ansible-pull -d`) и убить процессы AP'а, чтобы не было сложностей дальше - если консул не успеет приехать с дефолтными конфигами, делать ничего не надо. Если не успели убить AP до приезда консула - `apt-get remove --purge yandex-vertis-consul; rm -rf /opt/consul /etc/consul/conf.d/*;`.
2. Раскатываем конфиги через ansible (при необходимости - меняем хосты на нужные в соответствующем конфиге), все сервера рестартим.
3. Меняем на одном хосте в `/etc/consul/conf.d/config.json` - `acl:false`, `service consul restart`, `consul members -wan` - проверяем, что видим все остальные сервера. Должна так же появиться UI по адресу `<servername>:8500/ui`. Возвращаем `acl: false`.
4. Бутстрапим сервера (получаем токены). В конфиге консула на одном хосте выставляем `bootstrap: true`, рестартим консул. Выполняем команду `consul acl bootstrap`, мы получаем первичный токен. Сразу перекладываем его в секретницу и логинимся с ним в UI в разделе ACL. Возвращаем `bootstrap: false`, рестартим консул на хосте.
5. Создаем `ACL replication token`, `Master token` через UI с policy `Global Management` (как у Bootstrap токена); Создаем `default` и `monitoring` токены с идентичными тестингу policy; создаем токен consul-агента по [официальной доке](https://learn.hashicorp.com/tutorials/consul/access-control-setup#create-an-agent-token-policy)
6. Раскладываем получившиеся токены в секретницу и в конфиги ансибла в роли `consul-dev` - в соответствующие поля в конфигах для common-серверов, обычных серверов и агентов.
7. Раскатываем конфиги, рестартим сервера по очереди, проверяем логи консула.

[Дашборд по dev-consul-common](https://grafana.vertis.yandex-team.ru/goto/RrhGcTJnk?orgId=1)

Далее consul-сервера:
1. Повторяем шаги 1-2 из инструкции для consul-common серверов.
2. В один из конфигов серверов из другого ДЦ, который уже налиты, добавляем в поле `start_join_wan` один из серверов нового ДЦ, рестартим этот сервер, проверяем, что добавились новые сервера - `consul members -wan`. Это необходимо, чтобы старый датацентр увидел новый.
3. Проверяем логи новых серверов. Проверяем, что они появились в UI консула.

*Дашборда пока нет*

## Разворачиваем nomad-сервера

Плейбука: [vertis_vdev_nomad](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vdev_nomad.yml)

1. В UI консула создаем policy для номад-серверов по аналогии с тестингом и выпускаем токен для номад-серверов с этой policy. Токен кладем в конфиг номад-серверов в блоке `consul`.
2. Разворачиваем номад-сервера в терраформе. Сразу заходим на них и останавливаем ansible pull через `vertis-ansible-pull.sh -d` и убиваем его процессы.
3. Прогоняем кластерную плейбуку по всем номад-серверам.
4. Отключаем acl через конфиг на одном из номад-серверов, рестартим номад. Проверяем, что кластер собрался - `nomad cluster members`. Проверяем в UI консула, что номад-сервера в нем зарегистрировались.
5. Включаем acl обратно, начинаем бутстрапить сервера. Выполняем `nomad acl bootstrap`. Сохраняем токен и Accessor ID в секретницу. Создаем еще один токен для мониторинга и подкладываем его в тимплейт `nomad-monitoring.properties` в роли `nomad-servers-dev`. Раскатываем.
6. Проверяем наличие UI номада по адресу `<fqdn номад-сервера>:4646/ui`.
