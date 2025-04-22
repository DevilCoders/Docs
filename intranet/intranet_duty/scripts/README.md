# Автозаведение инцидентов

## Завести алерты через мониторадо
Смотри директорию `/alerts`. Правила которые там указаны позволят пройти эту инструкцию без проблем.

## Вручную

Сейчас все делается вручную, достаточно непросто. См секцию "автоматически".

### Зарегистрировать сервис в дежсмене поиска (MartyDB)
Добавить свой сервис сюда если еще нет https://workplace.z.yandex-team.ru/martydb#vertical=intranet 

Чтобы добавить новый сервис:
1. Нажать `add service`, указать вертикаль `intranet`, указать логин ответственного, слаг abc сервиса, указать название. ABC сервис выбирайте тот же самый, который выбран для имени директории с алертами. Прокрутить до низа и поставить галочки про назначение исполнителем дежурного.
2. Добавить в поле `Calendar` ссылку на вкладку [График дежурств в ABC](https://abc.yandex-team.ru/services/intranetduty/duty/) - откуда будет браться дежурный, причем ссылка должна быть на Дежурство по Интранету. Если вам по каким-то причинам нужно указать другой график дежурств - уведомите [команду разработки Дежурства по интранету](https://abc.yandex-team.ru/services/intranetduty/?scope=development). 
3. Добавьте графиков в `Charts`. Обязательно добавьте [стандартный шаблонный](https://a.yandex-team.ru/arc/trunk/arcadia/intranet/intranet_duty/templates?rev=6260303) и можете добавить своих. Там могут быть ссылки на `yasm`, `golovan`. Когда вы их добавите, в момент автоматического заведения тикета будут делаться скриншоты этих графиков и прикладываться в тикет. Примеры:

![1](https://jing.yandex-team.ru/files/smosker/2019-12-28_12-37-44.png)

![2](https://jing.yandex-team.ru/files/smosker/2019-12-28_12-38-09.png)

Внимание - сервис принимается на поддержку общим дежурным только если скрипт [Проверить количество срабатываний сигналов сервиса за неделю](https://a.yandex-team.ru/arc/trunk/arcadia/intranet/intranet_duty/scripts/notifications_count.py)
не выдает вам предупреждение о превышении допустимого количества.

### Зарегистрировать в джаглере уведомление  

Открыть https://juggler.yandex-team.ru/notification_rules/ нажать `Create`. Заполнить так:
* `selector` - можно взять из урла алерта примерный вид `host=yasm_directory_external_prod_5xx&service=directory_external_prod_5xx`
* `тип`  - `Push`
* `namespace` - ваше `namespace`, если еще не завели - завести вот тут https://juggler.yandex-team.ru/namespaces/
* `url` - `https://tickenator.yandex-team.ru/api/tickenator.services.TickenatorService/createTicketSPIAuto`
* `description` - описание в свободной форме

### Готово

Все! Теперь при CRIT по указанному алерту будет заводится тикет в SPI вида https://st.yandex-team.ru/SPI-8352 Так же в телеграмм в `tools_alarms` (!!пока не настроено!!) будут приходить уведомления о новых инцидентах.

# Автоматически

Когда сойдется задача https://st.yandex-team.ru/TOOLBOX-60 нужно будет 
1. Зарегистрировать сервис в MartyDB
2. Указывать на глобальном уровне всех YML конфигов мониторадо:
```
juggler_checks_defaults:
  tags: ['auto_ticket_creation']
```
3. И все!


## Полезные скрипты

[Настроить автозаведение через апи](https://a.yandex-team.ru/arc/trunk/arcadia/intranet/intranet_duty/scripts/auto_tickets_creation.py)

[Проверить количество срабатываний сигналов сервиса за неделю](https://a.yandex-team.ru/arc/trunk/arcadia/intranet/intranet_duty/scripts/notifications_count.py)
Пример вызова
```
OAUTH="token" SERVICE="forms" python3 notifications_count.py
```

## Работа с namespace
Namespace заводится вот [тут](https://juggler.yandex-team.ru/namespaces/), не забудьте указать в `owner` кроме сотрудников сервиса еще и  `robot-yasm-golovan`

Сменить namespace у существующих проверок через апи. При заведении проверок указывается дефолтный namespace - если у вас своего не было, то придется вручную менять его у всех проверок. Что не менять руками есть [вот такой код](https://a.yandex-team.ru/arc/trunk/arcadia/intranet/intranet_duty/scripts/change_namespace.py)

*Видео* - https://jing.yandex-team.ru/files/smosker/autoalert.mov

Пример вызова для настройки автозаведения алерта по одному сигналу
```
create_auto_alerts(
    selector='host=yasm_directory_internal_prod_mail_migrations_errors&service=directory_internal_prod_mail_migrations_errors',
    namespace='directory',
)
```

# Доступы

Запросить доступы в IDM до QLOUD балансеров для общего дежурного.
1. Исправь переменную balancers в файле idm_balancer_access.py.
2. Запусти файл `OAUTH="XXXX" python idm_balancer_access.py`.
