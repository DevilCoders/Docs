## Сервер
### Установка на новый сервер
#### Наливка железки через setup
Поправить по надобности
https://setup.yandex-team.ru/#!/configs/view/noc-rt-staging-ubuntu-20.04

#### salt
Салтификация живёт в nocdev salt-e [arcadia/admins/salt-media/noc/roots/nocdev-staging.sls](https://a.yandex-team.ru/arc_vcs/admins/salt-media/noc/roots/nocdev-staging.sls)

##### pillar
Первым делом нужно поправить `pillar`-ы в `noc/pillar/nocdev-staging.sls` и `noc/pillar/nocdev-mysql.sls` так как там есть маппинги shortname на CNAME в yandex-team.ru домене и id серверов mysql.

Сразу после наливки через setup и правки `pillar`-во на машинку нужно поставить конфиги для salt-а
```
apt update
apt install config-noc-salt-minion
```
Этот пакет притащит и настроит `salt-minion`
Дальше накатываем салтификацию
```
salt-call saltutil.sync_all saltenv=trunk
salt-call state.highstate
```

Салтификация сделает следующее
- поставит и настроит `docker` свежий докер
- притянет все нужные `docker images` из `noc-gitlab` и не только
- создаст необходимых юзеров и притянет нужные секреты
- создаст `zfs` пул `rt-zpool` и примонтирует все нужные `fs`
- поставит пакет `rttestctl` и сделает конфиг к нему
- сварит конфигу для контейнера `rt-mysql-main` и подготовит для него секреты

Дальше при первом запуске сервиса `rttestctl`, он в свою очередь поднимет докер контейнеры из `main set-а`.
Контейнер `rt-mysql-main` проверяет, что в каталоге `/rt-zpool/rt/mysql/`, который в контейнере монтируется в `/var/lib/mysql`, есть файл `my-resetup.state`.
Если в этом файле в json-e есть подстрока `"finished"`, то утилита `my-resetup` выходит, если такой подстроки нет, то запускается переналивка mysql со слейва.
Дальше налитый mysql подцепляется каскадной нодой к одному из слейвов. Контейнер будет полноценным участником кластера `mysync - racktables-stable`.
В контейнере после переналивки будут работать три демона `supervisord`, `mysqld`, `mysync`.

### dns имена, CNAME-ы и имена в кондукторе.
Именование нод стеджинга следующее.
- в боте железка должна иметь имя по шаблону [как тут](https://wiki.yandex-team.ru/noc/hld/noc-hld/#naimenovanija), но немного проще `<DC>-rt-staging<N>.net.yandex.net`
- хостнеймы ноды должен быть так же по шаблону
- в кондуктор добавляем имя хоста по шаблону
- CNAME-ы `*.nN.test.racktables.yandex-team.ru` -> `nN.test.racktables.yandex-team.ru` -> на имя по шаблону

`N` из `nN.test...` не обязательно соотвествует `N` из `...staging<N>`

Меняем n1 на ближайшую свободную запись
```shell script
dns-monkey.pl --zone-update --zone "test.racktables.yandex-team.ru" --expression "add-cname n1.test.racktables.yandex-team.ru dc-rt-staging1.net.yandex.net."
dns-monkey.pl --zone-update --zone "test.racktables.yandex-team.ru" --expression "add-cname *.n1.test.racktables.yandex-team.ru. n1.test.racktables.yandex-team.ru."
```

### Кондуктор
Новый хост должен быть добавлен в кондукторную группу `%nocdev-staging` либо `%nocdev-test-staging`.
После этого переприменяем конфигурацию для `test.racktables.yandex-team.ru` (`pre.test.racktables.yandex-team.ru` для тестовых нод) в l3-manager дабы обновился список рилов,
после этого дергаем на новой машинке сеть дабы появился тоннельный интерфейс.

# Финальные проверки
Пробуем запустить новое окружение на указанной ноде(описано в начале страницы). Если что-то не получается - читаем логи `journalctl -eu rttestctl` и логи контейнеров `docker logs <container>` и фиксим.

Проверяем, что прилетающие в docker-контейнер nginx-main health-check-и получают в ответ 200.