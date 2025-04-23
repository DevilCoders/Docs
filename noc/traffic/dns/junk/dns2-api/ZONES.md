#
#
#

0. Определения

      Бекенд "ns3+ns4" - текущая классическая схема с мастерами в dns-core,
      для которой slave сервера AUTH, CACHE используют AXFR/IXFR, для unbound
      и bind конфигураций.

      Бекенд "ns+yp" - перспективная схема для AUTH, CACHE периметров, со
      схемой хранения конфигураций зон в YP и репликами через unbound yp модуль.
      Оба бекенда используются одновременно на текущем этапе. Между ними
      включены синхронизации и dns2-api updates.

      Класс зоны - это набор конфигуриаций и расположений данных, который
      определяет полиси для WRITE, READ опереаций и конфигураций. Следующие
      классы выделены и в дальнейшем используются.
      
      Z0 - классическая схема, в которой BACKENDS: "ns3+ns4", FRONTENDS: "ns3+ns4",
           ACTIVATED: "ns3+ns4". Зоны, данные и конфигурации которые хранятся только
           в "ns3+ns4" бекенде с использованием только в AUTH периметре.

      Z1 - схема Z0, в которой добавляется контур CACHE, схемы хранения и
           конфигурации зон не меняются. Устаревший механизм, используется для
           тестовых конструкций.

      Z2 - основная схема, в которую зоны попадают после процедуры миграции c 
           определением: BACKENDS: "ns+ns4, ns+yp", FRONTENDS: "ns+ns4, ns+yp"
           ACTIVATED: "ns+yp,ns3+ns4". Фактически в dns2-api update и dns2-api
           sync происходят синхронизация двух BACKENDS с основным источником
           "ns3+ns4" -> "ns+yp". Все данные доставляются до AUTH и CACHE периметров,
           но фактически чтения данных не происходит.

      Z3 - схема Z2, в которой чтение происходит из реплики "ns3+ns4" в обоих
           периметрах AUTH, CACHE

      Z4 - основная, перспективаная схема, в которую все зоны класса Z0 проходят
           через операции MIGRATION, ACTIVATION (см. ниже). Это схема Z2, в
           которой все чтения выполняются из реплик "ns+yp", по сравнению с Z2
           меняется ACTIVATED: "ns+yp"

      Z5 - схема для зон, авторитеты которых находятся на YP. Зоны не участвуют
           в "ns3+ns4", прозрачно выпилены из конфигураций и отображются в конфигурациях
           в контуре CACHE. Технически выпиливаются как infrastrcture=qloud 
           а также список прямых YP зон (*.yp-c.yandex.net, ... , смотри dns2-api.yaml)

1. Приводим в соответствие текущий стейт зон в желаемый таргет Z2|Z4

      Зоны могут находится в одном из состояний Z0,Z1,...,Z5 а также Z*. Состояние
      определяется по конфигурациям в трёх источниках Z, M, Y. Z - это конфигурация
      зоны в dns-api dynamic zones (zookeeper), M - это meta конфигурация зоны, которая
      говорит в каких BACKENDS, FRONTENDS, ACTIVATED позициях зона в текущий момент,
      Y - присутствие зоны в YP BACKEND. Конфигурации зоны Z и M используются dns2-api 
      для выбора списка BACKEND для записи и синхронизации, а d2 для формирования
      конфигураций в dns-core MASTERS и dns нодах на CACHE и AUTH периметрах:

         dns2-api zone configuration analyze|apply --target="Z2|Z4"
            [--zone="*.arpa|*.id-addr.arpa|..."  or --origin="Z0|Z2" ]
            [ --dry-run] --debug

      Зона должна пройти миграцию или активацию из текущего состояния (Z0 или Z1)
      в состояние указанное в команде (--force --target="Z4") либо вычисленное
      автоматически. Автоматически вычисляютс следующие переходы: Z0 -> Z2,
      Z2 -> Z4. В некоторых случаях когда контент зон не важен можно сделать 
      override и добавить Z0 -> Z4:

      MIGRATION (Z0|Z1 -> Z2): origin состояние [Z][ ][ ] при выполнении для зоны
      последовательно делаются следующие шаги (1) создаётся конфигурация Y и команда
      ожидает появление зоны в списке YP BRIDGE (2) создаётся meta конфигурация
      в соответствии с таргетом

      ACTIVATION (Z2 -> Z4): зона находится в реплицированном на все контуры 
      состояние. Операция переводит конфигурацию контуров CACHE, AUTH когда
      операции чтения запросов выполняется из "ns+yp"

      SKIP - некоторые зоны по списку конфигурации не участвуют в операциях
      по переконфигурации

      Z2 - [Z][ ][Y], BACKENDS: "ns3+ns4", "ns+yp", FRONTENDS: "ns3+ns4", "ns+yp"
      ACTIVATED: "ns3+ns4". То есть зона находится в двух бекендах и данные её
      реплицируются как в AXFR/IXFR режиме так и YP на все контуры CACHE и AUTH.
      Обработка запросов на чтение выполняется из "ns3+ns4"

      Z4 - [Z][M][Y]: состояние Z2 + чтение выполняется из "ns+yp" в CACHE и AUTH
      наше окончательное целовое состояние для всех зон

      ПРИМЕРЫ:

      * формируем текущий стейт для зон Z, M, Y для всех зон (прямых и обратных)

         [~] dns2-api zone configuration analyze --debug --dry-run

      * формируем стейт Z, M, Y для обратных

         [~] dns2-api zone configuration analyze --debug --dry-run --zone="*.arpa"
         [~] dns2-api zone configuration analyze --debug --dry-run --zone="*.in-addr.arpa"

      * формируем стейт для обратных с Z4 таргетом

         [~] dns2-api zone configuration analyze --debug --zone="*.in-addr.arpa" \
               --target="Z4" --force --dry-run

      * применяем сформированные операции для обратных зон (skip операции не выполняются)

         [~] dns2-api zone configuration apply --debug --zone="*.in-addr.arpa"\
               --target="Z4" --force

2. Создаём зоны (или список зон) в желаемом классе Z0, Z2, Z4

      Перед созданием или удалением зоны, выполяется процедура получения стейта
      всех зон из источников конфигураций Z, M, Y. И проверяется существует ли
      хотя в одной из конфигураций зон. Уточнить что делать с [N] ...

         dns2-api zone create [--debug] --zone="$zone1" --zone="$zone2" ...
             --target="Z0|Z2|Z4" --realm="$realm" [--acl] [--force] [--dry-run]
             [--subject "$subject1" --subject="$subject2" ... ] [--now]

      ПРИМЕРЫ:

      * создать зону класса Z0 "google.yandex.net" с acl существующего realm'а
        (в этом случае зона создаётся в realm zone "realm-unclassified" и добавляется
        к существующему realm acl c owner "realm-tanks". Возвращается ошибка если
        указанного realm owner acl нет

        [~] dns2-api zone create --debug --zone="google.yandex.net" \
             --target="Z0" --realm="realm-tanks" --acl --dry-run

      * создать зону класса Z0 в legacy режиме (без acl) в соответствующем realm'е,
        здесь чтобы преодолеть запрет на создание зон в legacy mode следует указать
        флаг --force. Такое иногда может понадобится чтобы что-то там по-быстрому
        наколбасить и не думать.

        [~] dns2-api zone create --zone="google.yandex.net" --debug --dry-run \
             --target="Z0" --realm="realm-tt" --force

        [~] dns2-api zone create --zone="ravel.yandex.net" --debug  --target="Z0" \
             --realm="realm-security" --force

        [~] dns2-api zone create --realm="realm-keykeepers" --debug --target="Z0" \
             --zone="2a02:6b8:0:6709::/64" --zone="2a02:6b8:0:670a::/64" \
             --dry-run --force

        [~] dns2-api zone create --realm="realm-vladimir" --debug --target="Z0" \
             --zone="0.0.d.2.c.0.8.b.6.0.2.0.a.2.ip6.arpa" --dry-run --force

      * создать зону класса Z0 "yahoo.yandex.net" с новым acl с указанным списком
        subjects и realm acl owner'ом (предолагается что acl будет создан
        в процессе создания зоны. Выполяется проверка на то что укзанный realm owner
        существует, в случае существования изменения вносят в **существующий** acl

        [~] dns2-api zone create --debug --zone="yahoo.yandex.net" \
             --target="Z0" --realm="realm-kolbasa" --acl \
             --subject="svc_dostavkatraffika_administration" \
             --subject="svc_testingtoolsops_administration" \
             --dry-run

      * основной случай -- создаем зоны класса Z4 в сущестувующем acl, процесс для 
        каждой зоны состоит из 4 операций: (1) создать зону в Z, (2) создать зону в Y,
        (3) обновить ACL (4) добавить META конфигурацию, отражающую класс Z2 или Z4 

        [~] dns2-api zone create --debug --target="Z4" --realm="realm-keykeepers" --acl \
             --zone="2a02:6b8:82:280f::/64" --zone="2a02:6b8:82:7d12::/64" --now

3. Удаляем зоны (либо демонитируем зоны до желаемого класса)

      В процессе удаления зоны, по списку acl матчится те, в которых
      зона присутствует и создается список операций на изменение acl,
      которые матчатся с этой зоной, если задан флаг --acl. Проверяется
      полное совпадение зоны.

         dns2-api zone remove [--debug] --zone="$zone1" --zone="$zone2" ...
             [--target="Z0|Z2|Z4"] [--acl] [--force]
             [--dry-run] [--now]

      ПРИМЕРЫ:

      * удалить зону, класс зоны и какие конфигурации нужно удалить
        определяется автоматически, в следующем порядке Y, M, Z, для
        демонтажа класса с Z4 до Z2 нужно использовать DEACTIVATION,
        для Z2 -> Z0 REMIGRATION. Используем --now чтобы обновить текущий
        кеш зон и объектов  

        [~] dns2-api zone remove --debug --zone="tt.yandex.net" \
              --dry-run --now

      * удалить зону из динамической части Z и убрать вхождение зоны
        из указанного acl c owner "realm-tanks", зона из cidr представления
        перековертируется в arpa нотацию

        [~] dns2-api zone remove --debug --zone="2a02:6b8:1:670a::/64" \
              --target="Z0" --realm="realm-tanks" \
              --acl --now

      * основной случай - убираем зону из всех конфигураций: Z, Y, M, A, для 
        этого сформируются все 4 операции и последовательно выполнятся. Ключ
        now означает что мы перекешируем используемые источники, так чтобы
        получить текущее актуальное состояние, а не состояние кеша на момент
        его последного обновления (~10-20 минут)

        [~] dns2-api zone remove --debug --target="Z4" --realm="realm-keykeepers" --acl \
             --zone="2a02:6b8:82:280f::/64" --zone="2a02:6b8:82:7d12::/64" --now

      * удалить ACL с указанным uuid, может потребоваться когда сам acl
        стал ненужным или с пустым множеством namespace

        [~] dns2-api acl remove --uuid="1a928641-6bf8-48ce-b9ac-d931cad8a378" \
              --debug --dry-run

4. Операции по ACL синхронизации зон и namespaces (неразобрано)
# deleting 2a02:6b8:c2d::/56 (without acl)
dns2-api zone remove --zone="0.0.d.2.c.0.8.b.6.0.2.0.a.2.ip6.arpa" --debug --target="Z0" --realm="realm-vladimir" --force

# adding 2a02:6b8:c2d::/48 (without acl)
dns2-api zone create --zone="2a02:6b8:c2d::/48" --debug --target="Z4" --realm="realm-vladimir" --force

# merging acl realm zone into namespace notation
dns2-api acl merge --realm="realm-tanks" --debug --dry-run
dns2-api acl merge --realm="realm-corpservices" --debug --dry-run

# simplifying version, networks list configured from dns2-api.yaml
dns2-api acl sync --realm="realm-corpservices" --debug --dry-run

# adding zones to corp-services Z4 + acl
dns2-api zone create --zone="2a02:6b8:0:5710::/64" --zone="2a02:6b8:82:2890::/64" --zone="2a02:6b8:82:7890::/64" --debug --target="Z4" --realm="realm-corpservices" --acl --dry-run

# making dns-core dynamic master cluster configuration update
# using ACTIVE node cluster
d2 master config update --class="ns3+ns4" --debug --dry-run

# updating slave instances (CACHE + AUTH)
d2 slaves config install --class="ns3+ns4+others" --location="man"...."mskm9" --debug

# updating delegation records dns-core static master cluster
# using ACTIVE node cluster
dns2-api mgmt pipeline markup --zone="0.0.0.0.8.b.6.0.2.0.a.2.ip6.arpa" --debug --dry-run

# syncing acl zones and namespaces with RT zones.xml, commands generated by
dns2-api acl sync --debug --dry-run --foreground

dns2-api acl sync --realm='realm-tanks' --debug
dns2-api zone remove --debug --zone=2a02:6b8:b040:1a00::/56 --zone=2a02:6b8:0:a1c::/64 --target='Z4' --realm='realm-yt' --acl
