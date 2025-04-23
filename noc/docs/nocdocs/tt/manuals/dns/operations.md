# Типовые операции
## Переключение мастера ns3+ns4/ns1+ns2
[Актуальная инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/noc/traffic/dns/junk/d2/README.md) "d2 promote master tasks:" и внутри блока нужен "(F) algorithm version 2". Нюансы:
- команды выполняются исключительно на мастерах:
  - для динамики dns-core01[i,s,v].berry.yandex.net + alpha-30v.lxd.tt.yandex.net(по типу дев. сервера)
  - для статики dns-core02[i,s,v].berry.yandex.net + alpha-33v.lxd.tt.yandex.net(по типу дев. сервер)
- в первом пункте команда выполнятся на всех dns-core нужной роли и в качестве параметра мастера указывается старый мастер
- второй и третий пункт - безопасные команды, делаются на всех нодах за исключением старого мастера
- в четвертом пункте указывается новый мастер и выполняется на всех dns-core нужной роли
- пункт пятый остаётся под вопросом, т.к. нужно выбрать какую-то машину, на которой считаем, что d2 конфиг актуальный, поменять в нём и раскатать, как раскатать вопрос пока тоже открытый
- полезные графики находятся [тут](https://grafana.yandex-team.ru/d/611b_yUWz/ns1-ns2-ns3-ns4-metrics?orgId=1&refresh=1m&var-class=ns3-ns4&var-location=vla) и [тут](https://grafana.yandex-team.ru/d/611b_yUWz/ns1-ns2-ns3-ns4-metrics?orgId=1&refresh=1m&var-class=ns1-ns2&var-location=vla) с названием "zone config diff"

Видео, как переключить мастер [ns1+ns2](https://jing.yandex-team.ru/files/slayer/dns-core-staticmaster-switch.mkv) и [ns3+ns4](https://jing.yandex-team.ru/files/slayer/dns-core-dynamicmaster-switch-4.mkv) на примере переключений из `VLA` в `SAS`

## Изменения записей в зонах
Основные заповеди(дополняются по мере опыта):
```
- не делаем персональных записей в зонах TLD(Top Level Domain)
- если за динамическую зону мы явно не отвечаем, и есть группа и/или робот перенаправляем к ним
- на одном уровне с CNAME не должно быть других записей(напр: TXT/MX/etc)(https://support.dnsimple.com/articles/cname-record/#restrictions)
- не делаем wildcard для AAAA записей, следует использовать CNAME в этом месте
- проверяем, что cname который хотят не от целой зоны, такие просим педелелать на А/АААА записи
- обращаем внимание на изменение вайлдкардов или если открываем зону а записи в ней нет(стоит искать вайлдкард в том числе в зоне выше)
- для людей которые хотят прописать внешние адреса/CNAME в наших зонах особенно yandex.ru, yandex-team.ru — требуется approve от СИБ
- зоны из списка ниже управляются не нами и нужно отправлять к владельцам(/etc/d2/d2.yaml->configuration.zones.dynamic-zones.excluded.zones):
  zones: [ "*.yp-c.yandex.net", "gencfg-c.yandex.net", "in.yandex.net", "yp-test.yandex.net", "qloud-b.yandex.net", "qloud-c.yandex.net", "qloud-d.yandex.net", "in.yandex-team.ru" ]
```
### Изменения в динамических зонах
1. нужны права на изменения зон. В большинстве случаев нужно находится в dpt_yandex_mnt_dns_supporters(которой больше нет) или dpt_yandex_mnt_traf
2. для изменения используем dns-monkey - https://wiki.yandex-team.ru/dynamic-dns/ Команды в помощь:
```bash
# операции по добавлению и удалению в4/в6 А/АААА/CNAME/PTR записей
dns-monkey.pl --zone-update --expression "add-a dist01ft.yandex.net 2a02:06b8:0000:1449:3659:4e0d:6e98:8f8b" -debug
dns-monkey.pl --zone-update --expression "add-aaaa vs-stmongo01ht.yandex.ru 2a02:06b8:0000:1a1e:2337:4c43:8be6:6cda" -debug
dns-monkey.pl --zone-update --expression "add-cname dukeartem01i.yandex.net. dukeartem01i.tools.dev.yandex-team.ru." -debug
dns-monkey.pl --zone-update --expression "delete-ptr 95.108.230.29 otrs-shard01-dbs.tools.yandex.net" -debug
dns-monkey.pl --zone-update --expression "add-ptr 2a02:06b8:0000:1449:3659:4e0d:6e98:8f8b dist01ft.yandex.net" -debug
dns-monkey.pl --zone-update --expression "delete-ptr 93.158.156.10 svn-gpfs-01.yandex.ru" -debug
# добавить сразу прямую и обратную зоны
dns-monkey.pl --zone-update --expression "add sber-m9-proxy01u.market.yandex.net 2a02:6b8:0:2011:52f6:5e4a:0643:b669" -debug
# удалить сразу прямую и обратную зоны
dns-monkey.pl --zone-update --expression "delete sber-m9-proxy01u.market.yandex.net 2a02:6b8:c04:176::577:52f6:5e4a" -debug
# интерактивный вывод(открывается vim в котором можно сразу несколько мест поправить
dns-monkey.pl --zone-update --zone vs.os.yandex.net. --interactive -debug
#  информация о зоне(доп. кто может её редактировать)
dns-monkey.pl --zone-info --zone "tools.dev.yandex-team.ru"
# какие зоны прикреплены к vlan
dns-monkey.pl --vlan-info --vlan 1307
```
3. diff изменений прикладываем в тикет

### Изменения в статических зонах
1. нужны доступы до мастеров %dns-core-statc
2. /etc/d2/d2.yaml - посмотреть кто мастер можно в конфиге на машинах мастеров(core.cluster.static.master)
3. /etc/named/master - тут нужно найти статическую зону требующая изменений
4. меняем любым консольным редактором
5. делаем make -f Makefile-Zone %имя_зоны_без_.m4%  из /etc/named/ и проверяем diff
6. /var/log/named/named-messages.log - содержит информацию что изменения разъезжаются

### Поменять acl зон
1. инструкция:
   1. для редактирования нужен dns2-api, который например доступен на alpha-31v.lxd.tt.yandex.net
   2. для расширения существующих доступов, сначала сохраним текущие `dns2-api acl list -T > /tmp/acl.list`
   3. найдя в `/tmp/acl.list` нужные группы возьмём оттуда UUID и отредактируем в интерактивном режиме `dns2-api acl edit --uuid="43e8b6c9-e443-4ce0-be17-...."`
   4. после сохранения всё автоматически применится, из нюансов: паттерны `(.*)` не очень паттерны и скорее зарезервированная конструкция
2. краткие заметки:
    - [dns2-api README.md](https://a.yandex-team.ru/arc/trunk/arcadia/noc/traffic/dns/junk/dns2-api/README.md) содержит примеры команд для изменений acl
    - где выполнять - обычно на фронтах dns-api, группа %dns-dnsapi
    - dns2-api acl list - покажет содержимое нового хранилища версий acl (dns-ui информацию получает отсюда же)
    - часть acl находится всё ещё в старом хранилище на dns-core (Олег занимается переносом в новое)
    - если не уверен в действиях, везде есть --dry-run
    - в /etc/dns2-api/ некоторые acl записаны в статистические конфиги
    - topology хранится в yav и управляется облаком(сущность должна упраздниться и переехать в acl)
    - ответственные за обратные зоны берутся из RT
    - остальные объекты хранятся в зукипере
    - какая-то информация есть тут https://st.yandex-team.ru/TRAFFIC-11479


## Добавить новую динамическую зону
По мотивам https://st.yandex-team.ru/TRAFFIC-12684 и проделанного руками:
- зоны заводятся в очереди https://st.yandex-team.ru/HOSTMASTER и в какой-то момент призывается Олег, которого просят завести их на ns серверах
- https://wiki.yandex-team.ru/LegalDep/domain/monitoring/ таблица, где робот поддерживает информацию о статусе домена и по которой он актуализирует статус тикета
- делается на alpha-31v.lxd.tt.yandex.net потому что он "тестинг" для dns2-api или на серверах dns2-api
  `dns2-api zone create --target="Z4" --realm="realm-market" --acl  --zone="sphere360.yandex" --debug --dry-run`
  - в realm если непонятно кто ответственный, можно поставить realm-unclassified, список acl можно посмотреть `dns2-api acl list -T | less`
  - команда подготовит некоторую метаконфигурацию и структуры с правами
- делается на мастере ns3+ns4 из группы %dns-core
  `d2 master config update --class="ns3+ns4" --debug --dry-run`
  - создаст новые зоны и другие нужные на мастерах и в yp конфиги/структуры
- раскатываем на CACHE + AUTH
  - на мастере dns-core берём команды из /etc/named/Makefile
  - сначала раскатываем на prestable: строка `remote-update-prestable:` и команды `d2 slaves config install --class="ns3+ns4+others" --location="alpha...ams" --debug;`
  - а потом на stable из `remote-update-all:` и `remote-update-ns-cache:` по одной команде: `d2 slaves config install --class="ns3+ns4+others" --location="man"...."mskm9" --debug`
- робот, который призвали Олега в тикет HOSTMASTER находится во владение Олега и периодически проверяет статус доменов указанных в тикете и если они проросли, то отписывается в тикет и меняет их статус

## Удалить динамическую зону
- первая команда, вместо `dns2-api zone create...` пишем `dns2-api zone remove`, например
`dns2-api zone remove --debug --zone=2a02:6b8:b010:aa00::/56 --target='Z4' --realm='realm-stat' --acl
dns2-api zone remove --debug --zone="ps-cloud.yandex.ru" --target='Z4' --realm='realm-oebs' --acl`
- все остальные команды из [Добавить новую динамическую зону](https://docs.yandex-team.ru/nocdoc/tt/manuals/dns/operations#dobavit-novuyu-dinamicheskuyu-zonu) делаем без изменений
- Идём на  dns-core(active) static master, убираем делегирования из yandex.TLD, например
`# yandex-team.ru
-ps-cloud.yandex-team.ru.       IN      NS      ns3.yandex.ru.
-ps-cloud.yandex-team.ru.       IN      NS      ns4.yandex.ru.`

## Обновление unbound и конфигов
### RTC/Nanny

{% cut "старый способ" %}

- всё происходит на вкладке Files (напр. https://adm-nanny.yandex-team.ru/ui/#/services/catalog/production_dns_cache/files)
- CI/CD нет, поэтому все ресурсы собираются через sandbox по запросу
- на вкладке Files можно выйти на конкретную sandbox сборку выбранного ресурса, нажать склонировать, поменять ревизию на которой происходила прошла сборка и запустить
- изменения не раскатываются сразу на все контейнеры, а используя шестеренку перезапускаем по несколько контейнеров и проверяется глазками по логам как оно обновилось

{% endcut %}

- через ci/cd
1. выбираем ci/cd
   - [если обновляем unbound](https://a.yandex-team.ru/projects/dostavkatraffika/ci/releases/timeline?dir=noc%2Ftraffic%2Fdns%2Fci%2Funbound&id=release-unbound-to-rtc)
   - [если обновляем скрипты или конфиги](https://a.yandex-team.ru/projects/dostavkatraffika/ci/releases/timeline?dir=noc%2Ftraffic%2Fdns%2Fci%2Fconfigs_and_scripts&id=release-cs-to-rtc)
2. нажимаем `Run release`
3. если нужно удалить yp кеш на вкладке `Custom parameters` ставим галочку `Дропнуть YP-cache?`
4. запускаем кнопкой `Run release`
5. переходим в созданный пайплайн и наблюдаем за этапами(там где нарисован волшебник - требуется ручное подтверждение)
### Железные/lxc

{% cut "старый способ" %}

- ci/cd нет, версионирование конфигов тоже. Поэтому берём любую машинку, по типу build-bionic-01v готовим вручную бандл со всеми изменениями и катим скриптом аккуратно всё перезапуская

```bash
#!/bin/bash -x
deploy_hosts="ns01f.name.yandex.net ns02f.name.yandex.net ns03f.name.yandex.net ns04f.name.yandex.net ns05f.name.yandex.net ns06f.name.yandex.net"

root_dir="/home/dukeartem/unbound-dns64/"
config_dir="etc lib"

for dh in $deploy_hosts;
do
for d in $config_dir;
do
rsync -av ${root_dir}/${d} root@${dh}:/ --progress
done;
ssh root@${dh} "d2 slaves l3 disable --debug"
sleep 10
ssh root@${dh} "systemctl stop bind9-aaaa.service"
ssh root@${dh} "systemctl stop bind9-nat64.service"
ssh root@${dh} "systemctl stop unbound-dns64.service"
sleep 3
ssh root@${dh} "systemctl daemon-reload"
ssh root@${dh} "systemctl start bind9-aaaa.service"
ssh root@${dh} "systemctl start bind9-nat64.service"
ssh root@${dh} "systemctl start unbound-dns64.service"
ssh root@${dh} "/usr/sbin/unbound-control -s127.0.0.1@956 status"
sleep 30
ssh root@${dh} "/usr/sbin/unbound-control -s127.0.0.1@956 status"
if [ $? -ne 0 ];
then
exit 1
fi
ssh root@${dh} "d2 slaves l3 enable --debug"
done;
```
{% endcut %}

- через ansible
1. обнаружить новую сборку в [UNBOUNDREL](https://st.yandex-team.ru/UNBOUNDREL)
2. счекаутить репу с [ансиблом](https://a.yandex-team.ru/arc/trunk/arcadia/noc/traffic/dns/ansible)
3. поменять в playbooks/roles/unbound/vars/main.yaml
```
resource_url: http://s3.mds.yandex.net/sandbox-tmp/2888533985/unbound.1.15.0-r9250700.tar.gz
resource_version: 1.15.0-r9250700
```
на значения из сендбокс таски которой была собрана новая версия([для примера](https://sandbox.yandex-team.ru/resource/2888533985/view))
4. сначала выкатываем на prestable
`ansible-playbook -i hosts playbooks/name-update-unbound-and-unbound64.yaml --limit 'prestable'`
5. потом на один ДЦ
`ansible-playbook -i hosts playbooks/name-update-unbound-and-unbound64.yaml --limit 'name_iva'`
6. после проверки, что всё в порядке катим в stable на оставшиеся ДЦ
`ansible-playbook -i hosts playbooks/name-update-unbound-and-unbound64.yaml --limit 'stable:!name_iva'`
7. добиваем экспериментальный хост `ns02v.name.yandex.net` руками
8. **не забываем коммитить изменённый** `playbooks/roles/unbound/vars/main.yaml`
## Железные проблемы
### Как переливать srv машинки
!!TBD!!
### Вылет диска
!!TBD!!
## Про LXC/LXD
### Перевоз lxc контейнеров между dom0
Большой мануал https://wiki.yandex-team.ru/oleggoroxov/lxd-cdn/ в идеале его нужно распилить на сценарии
### Нюансы
- базовый образ для разных контейнеров хранится на машине srv02i.berry.yandex.net по команде `lxc list`

{% cut "роль каждой alpha-*.lxd.tt.yandex.net можно посмотреть в /opt/lxd-mgmt.pl на srv02i.berry.yandex.net" %}

```perl5
# Correspoding cdn-types and build containers
$config->{'build-contaters'}->{'cdn-proxy'}="alpha-02v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-static'}="alpha-01v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-cache'}="alpha-03v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-strm'}="alpha-04v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-slaves'}="alpha-07v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-redirects'}="alpha-08v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'cdn-base-focal'}="alpha-28v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'dns-selfdnsapi'}="alpha-29v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'dns-api'}="alpha-31v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'dns-core'}="alpha-30v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'dns-core-static'}="alpha-33v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'dns-cache'}="alpha-05v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'cdn-strm-xenial'}="alpha-09v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-strm-bionic'}="alpha-25v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'dns-authoritative'}="alpha-10v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'dns-dyn-authoritative'}="alpha-11v.lxd.tt.yandex.net";

# new versions of containers?
$config->{'build-contaters'}->{'dns-selfdns'}="alpha-34v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'dns-dynamic-hybrid'}="alpha-09v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'dns-yc'}="alpha-15v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'dns-api'}="alpha-31v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'dns-yp'}="alpha-12v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'dhcp-boot'}="alpha-32v.lxd.tt.yandex.net";

# dns load slaves - containers for load/tank should be a
# master and slave roles?
$config->{'build-contaters'}->{'dns-load'}="alpha-26v.lxd.tt.yandex.net";
#$config->{'build-contaters'}->{'dns-cfgd'}="alpha-27v.lxd.tt.yandex.net";

$config->{'build-contaters'}->{'cdn-zora'}="alpha-06v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-hx'}="alpha-20v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-rex'}="alpha-21v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-vhproxy'}="alpha-22v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'dns-cachedns'}="alpha-23v.lxd.tt.yandex.net";
$config->{'build-contaters'}->{'cdn-loadlb'}="alpha-24v.lxd.tt.yandex.net";
```
{% endcut %}

## Про наш GeoDNS

{% cut "принципиальная схема работы" %}

![schema 1](https://jing.yandex-team.ru/files/dukeartem/IMG_20220601_115436.jpg)
![schema 2](https://jing.yandex-team.ru/files/dukeartem/IMG_20220601_115908.jpg)

{% endcut %}

- vip ns1.taxi.yandex.net и ns2.taxi.yandex.net собран над серверами https://c.yandex-team.ru/groups/dns-taxi
- всё начинается с того, что мы не можем отдельные адреса завернуть на geodns, поэтому нужно выделить зону и делегировать её на ns[1,2].taxi.yandex.net (напр. tc.mobile.yandex.ru.) и зона даже для РФ обслуживается с геоднс серверов
- на каждом сервере крутится bind+geoip(база от maxmind)
- в /etc/bind/named.conf пишутся ACL которые группируют в себе страны по двухбуквенному сокращению
- в /etc/bind/named.conf пишутся view, которые по match-clients из ACL определяют должен ли в них провалиться ip. В каждом view должен быть описан полный набор зон, потому что запрос провалившись в них обратно не вернётся и должен обязательно отрезолвится в какой-то из зон. Соответственно у view есть иерархия от наименьшего покрытия к наибольшему и view "default" как покрывающию всё что не попало в другие. 
- каждая зона для каждого geo view описывается в отдельном файле в /etc/bind/zones/ 
- если нужно проверить в какую geo зону попадает ip можно выполнить `geoiplookup -i -d /etc/bind/geoip 77.67.174.24` - база давно не обновлялась, так что может и врать
- общей автоматики нет, каждый сервер конфигурируется руками индивидуально и делается `systemctl restart bind9` 
- в /var/log/named/named-query.log пишутся все запросы из которых можно понять всё ли идёт по плану и ответить на вопрос "почему наш ip не попал куда надо"
