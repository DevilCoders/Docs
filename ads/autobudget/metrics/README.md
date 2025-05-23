В этой директории лежат скрипты для расчёта метрик.

### Терминология
В нашей терминологии "метрикой" называется любая измеримая величина.

Метрики можно разделить на два типа:
1. KPI - Key Performance Indicators.
Во внешнем мире они обычно называются OKR (Objective Key Results), но в ОКР мы говорим не "OKR", а "KPI".
Мы целенаправленно работаем над тем, чтобы такие метрики менялись (например, чтобы росла доля денег или чтобы снижалось время до первого показа кампании).
Скрипты для расчета KPI должны иметь в названии суффикс `_kpi`.
2. Мониторинги. Это такие метрики, которые отслеживают состояние системы.
Мы обычно не работаем целенаправленно над тем, чтобы они менялись.
Для таких метрик мы устанавливаем определенный диапазон допустимых значений,
и выход из этого диапазона говорит о проблемах, которые надо чинить.
Мониторинги могут быть технические (например, отставание таблиц или объем потребляемых ресурсов на кластере) или продуктовые (например, перетраты в кампаниях с оплатой за конверсии).
Скрипты для расчета мониторингов должны иметь в названии суффикс `_monitoring`.

### Алёрты
Алёрты шлём в Juggler, потому что это более универсальная система.
В частности, там можно навесить алёрты не только на графики, но и на падения скриптов.

Соглашение для алёртов в Juggler (см. [документацию](https://abc.yandex-team.ru/services/cpaautobudget/)):
- namespace `autobudget`
- host -- имя скрипта
- service -- имя метрики

Аггрегации в Juggler настраиваются "на лету", ничего заводить в интерфейсе Juggler не нужно.

На весь неймспейс `autobudget` заведено [правило уведомлений в Juggler](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5ea2c7aeef162500732ccc56).

Вот так можно посмотреть на все проверки: [ссылка](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dautobudget)

Вот здесь можно получить токен для juggler: [ссылка](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0).

Токен сохраняется в переменную окружения `JUGGLER_TOKEN`

### Графики
В качестве бэкенда для графиков используем Solomon, т.к. он более надёжный.
При желании можно настроить отрисовку из Solomon в Grafana.

Соглашение для метрик в Solomon (см. [документацию](https://wiki.yandex-team.ru/solomon/userguide/datamodel/)):
- project `cpa_autobudget`
- service `monitorings`
- cluster -- YT кластер (почти всегда `hahn`) или близкая сущность
- label "monitoring_name" -- имя скрипта
- sensor -- имя метрики

Вот здесь можно получить токен для solomon: [ссылка](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1c0c37b3488143ff8ce570adb66b9dfa).

Токен сохраняется в переменную окружения `SOLOMON_TOKEN`
