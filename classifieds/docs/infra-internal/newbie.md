# Добро пожаловать

Во-первых, поздравляем с первым днем на работе!
Дальше будут полезные ссылки и описание важных для работы процессов и утилит.

Дополнения приветствуются.

## Что сделать первым делом

* Добавить на [staff](https://staff.yandex-team.ru) telegram-логин;
* Попросить ментора или руководителя добавить тебя в основные чаты;
* Добавить себя в [vertis-admin-bot](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-admin-bot/config.yml) для возможности дежурить;
* Посмотреть [доку про зоны ответственности](https://docs.yandex-team.ru/classifieds-ops-internal/areas-of-responsibility). Если в ходе работы будут возникать вопросы по работе с каким-либо из сервисов - можно обратиться к ответственным и задать им свои вопросы.

## Что почитать первым делом

* У Вертикалей уже есть общая страница знаний для нового сотрудника, начать чтение стоит именно с [нее](https://wiki.yandex-team.ru/verticals/newbie/).
* Сама страница Вертикалей на wiki [тут](https://wiki.yandex-team.ru/verticals/).
* DIY от helpdesk по настройке ноута, wifi и всевозможных тулов - <https://wiki.yandex-team.ru/DIY/>
* Страница инфраструктурных сервисов Яндекса - <https://i.yandex-team.ru>

Основную документацию нашей службы можно найти тут:
* [Vertical Services maintenance](https://wiki.yandex-team.ru/vertis-admin/) - старая *внутренняя документация*. Там можно найти много полезной информации о работе с различными инструментами. Ссылки на документацию на `wiki.yandex-team.ru` можно отправлять за пределы службы. Новую документацию на wiki мы не создаем;
* [Classifieds Infra Internal](https://docs.yandex-team.ru/classifieds-ops-internal/) - новая **внутренняя документация**, не делитесь ею за пределами службы. Новую внутреннюю документацию нужно писать именно здесь, а не на wiki;
* [Classifieds Infra](https://docs.yandex-team.ru/classifieds-infra/) - новая **внешняя документация**. Этой докой пользуются сотрудники за пределами нашей службы, поэтому ею можно делиться. В ней можно найти информацию о нашей системе деплоя и других инфраструктурных сервисах Вертикалей.

## Настройка оборудования

Чтобы приступить к работе нужно настроить окружение и рабочие инструменты на ноутбуке:

* Добавить ssh-ключ на staff;
[Тут](https://wiki.yandex-team.ru/diy/macos/ssh/) описана хорошая дока о том, как добавить ssh-ключ на staff и настроить ssh на ноуте.
Пример настроек .ssh/config:

```bash
Host *
   ForwardAgent yes
   AddressFamily any
   LogLevel ERROR
   UseKeychain yes
   AddKeysToAgent yes
   IdentityFile ~/.ssh/id_rsa
   SendEnv LANG LC_*
```

* Поставить и настроить [GoLand](https://www.jetbrains.com/ru-ru/go/);
Для активации используется [сервер ключей](https://wiki.yandex-team.ru/jetbrains/licenseservers/);
* Настройки для корректной работы go с приватными репозиториями:

```bash
git config --global url.git@github.com:.insteadOf https://github.com/
go env -w GOPRIVATE=github.com/YandexClassifieds
```

* Установить [ansible](https://wiki.yandex-team.ru/vertis-admin/howto/ansible-the-one/).
* Установить и настроить [terraform](iaas/terraform).
* Привезти docker и docker-compose на ноутбук.
* [Авторизоваться в yandex registry](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization).
* [Настроить VPN для работы с ресурсами CM.Expert](cme/cme-vpn.md).

Дальше только для ops, список тулов которые нужно установить на ноутбук:

* [executer](https://wiki.yandex-team.ru/executer/);
* [dns-monkeу](https://wiki.yandex-team.ru/dynamic-dns/dns-monkey-roadmap/).

## FAQ по типовым задачам

* [Работа с vertis-ansible и vertis-packages](iaas/ansible-and-packages)
* [Дежурства](duty/duty)
* [Заказ доступов](../infra/faq/access-request-faq)
* [Мониторинг](services/metrics-and-monitoring/juggler-monitoring)
* [Наливка серверов](iaas/metal-server-management.md)

## Основные информационные ресурсы

### Управление серверами
* `c.yandex-team.ru` - управление группами хостов, их именами и тэгами;
* `wall-e.yandex-team.ru` - управление докер-кластерами (переналивка и редеплой);
* `bot.yandex-team.ru/adm` - переименование, просмотр комплектации и преднастройка железных серверов;
* `setup.yandex-team.ru`, `https://eine.yandex-team.ru/` - наливка железных серверов;
* `racktables.yandex-team.ru` - работа с сетью на железных серверах;
* `qyp.yandex-team.ru` - виртуальные сервера в qyp;
* `console.cloud.yandex.ru` - внешнее Яндекс.Облако, `cloud.yandex-team.ru` - внутреннее Яндекс.Облако;
* `rundeck.vertis.yandex.net` - автоматизация периодических задач.

### Деплой
* `j.vertis.yandex-team.ru` - Jenkins;
* `nomad.vertis.yandex.net`, `nomad.test.vertis.yandex.net` - Nomad UI;
* `consul.vertis.yandex.net`, `consul.test.vertis.yandex.net` - Consul UI;
* `admin.vertis.yandex-team.ru` - админка деплоя;
* `yav.yandex-team.ru` - хранение секретов;
* `t.vertis.yandex-team.ru` - TeamCity;
* `zk.vertis.yandex.net`, `zookeeper.vertis.yandex.net` - Zookeeper.

### Мониторинг
* `grafana.vertis.yandex-team.ru` - логи и графики;
* `prometheus.vertis.yandex.net` - Prometheus с продовыми метриками, `prometheus-testing.vertis.yandex.net` - Prometheus с тестинговыми метриками;
* `jaeger.vertis.yandex.net` - трейсы;
* `juggler.yandex-team.ru` - алерты;
* `sentry.vertis.yandex.net` - Sentry.

### Другое
* `crt.yandex-team.ru` - сертификаты;
* `l3.tt.yandex-team.ru/service` - балансеры;
* `dns.tt.yandex-team.ru/request` - заявки на изменение DNS.

## Основные репозитории для работы
* [admin-utils](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-utils) - можно найти много тулов для админской работы. Самый часто используемые из них:
    * `qyp-mngr.sh` - наливка виртуальных хостов в qyp, в том числе dev-виртуалок;
    * `lxc-mngr.sh` - наливка lxc-контейнеров;
    * `project_id_nalivka.sh` - наливка железных хостов в нуля.
* [vertis-ansible](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible) - плейбуки и модули для ansible;
* [vertis-packages](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages) - поддерживаемые и собираемые нами пакеты;
* [ansible-juggler-config](https://a.yandex-team.ru/arc_vcs/classifieds/infra/ansible-juggler-configs) - конфиги алертов для Джаглера;
* [prometheus-config](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config) - алерты и recording-rules для метрик;
* [datasources](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/datasources/browse) - секреты для сервисов, которые живут в старом деплое;
* [services](https://a.yandex-team.ru/arc_vcs/classifieds/services) - все-все-все для сервисов (можно найти ответственных за сервисы и документацию);
* [terraform](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/terraform/browse) - конфиги для terraform для Яндекс.Облака;
* [packer](https://a.yandex-team.ru/arc_vcs/classifieds/infra/packer) - конфиги для сборки образов в Яндекс.Облаке.
