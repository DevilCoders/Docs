# Job

Основным объектом в Maxwell является job - задача поддержания/приведения группы хостов к нужному состоянию.

## Source/Filter

Позволяет различными вариантами задать множество хостов, над которым работает _job_. Т.к. сервис работает исключительно
с WALL-E, все атрибуты - исключительно берутся из WALL-E. Например, это может быть проект.

## Order

Отсортировать очередь работы. Можно сортировать по `[location, rack, hostname]`

## Group

Объединяем хосты в группы. Можно группировать по `[location, rack, hostname]`. Джоба в одновременно может обрабатывать
хосты только из одной группы. Например, при

```yaml
group:
    - location
    - rack
```

Одновременно будут обрабатываться только хосты из одной стойки

## Action

Что нужно сделать с хостом для приведения его к нужному состоянию задаётся типом тасков. Доступные варианты:

* `auto_firmware_update` - обновление прошивок (выбиравет один из типов тасков ниже в зависимости `walle_firmware`
  , `hostman-distrib`)
    * `drives_update` - обновление прошивок дисков ["SSD", "HDD", "NVME"]
    * `drives_update_with_redeploy` - обновление прошивок дисков ["SSD", "HDD", "NVME"] и переналивка
    * `firmware_update` - полное обновление прошивок
    * `firmware_update_with_redeploy` - полное обновление прошивок и переналивка
* `reboot` - перезагрузка (например, для обновления ядра)
* `auto_redeploy` - переналивка (например, для обновления дистрибутива) (выбиравет один из типов тасков ниже в
  зависимости `walle_firmware`, `hostman-distrib`)
    * `redeploy` - переналивка
    * `drives_update_with_redeploy` - обновление прошивок дисков и переналивка
    * `firmware_update_with_redeploy` - полное обновление прошивок и переналивка
* `auto` - полностью автоматический режим. По `['need_reboot_kernel', 'hostman-distrib', 'walle_firmware']` определяет
  какой action нужно запустить

## Window

* window
  > Количество одновременных тасков (хостов).
* audit_window
  > Колличество одновременных тасков в warn audit set При превышении `audit_window` джоба останавливается (не запускает новые таски)
  пока в warn audit set тасков больше чем `audit_window`

## Timeouts

* `timeout.cms (default=6h)` - таймаут таска с хостом со статусом `acquire-permission:cms`
* `timeout.itdc (default=6h)` - таймаут таска с хостом с тикетом в ITDC
* `timeout.default (default=3h)` - дефолтный таймаут таска

После превышения данных таймаутов хост попадает в warn audit set

# Safety level

* `safety_level=NORMAL` `ignore_cms=false`, валидация restrictions (ex. job с типом reboot должна запускаться с
  restrictions=['automation','automated-reboot','reboot'])
* `safety_level=IGNORE_CMS` `ignore_cms=true`, валидация restrictions
* `safety_level=IGNORE_ALL` `ignore_cms=true`, отключена валидация restrictions, после каждого успешного завершения
  таска sleep=2h

# Флаг ssh для reboot тасок

* `SSHForbid = "forbid"`, ssh режим для тасок ребута выключен
* `SSHOnly = "only"`, только ssh режим для тасок ребута
* `SSHFallback = "fallback"`, совместимый режим основной режим ssh c фолбэком на ipmi для тасок ребута

# Mode

* `script` - режим при котором хосты не берутся в работу повторно. Позволяет избежать циклических действий над одним
  хостом
* `follow` - режим слежения, в работу берутся все хосты, которые попадают под селектор

# Examples

Попробуем дать примеры для старта работы с сервисом. К сожалению, UI в зачаточном состоянии. Переходим на
страницу [создания job'а](https://maxwell.in.yandex-team.ru/create-job) и заполняем.

## Пример

````yaml
name: reboot-segment-prestable-def # Уникальное имя job'ы
window: 1 # Количество одновременных тасков (хостов)
windowOverflow: 0 # Максимальное колличество тасков (хостов) в ожидании (когда 0 - отключено)
source: # откуда брать исходное множество хостов
    walle:
        project: ''
        tags:
            - rtc.reboot_segment-prestable-def # например по такому wall-e tag'у
        location: ''
filters: # фильтруем то, что удалось достать с помощью source
    health:
        ok:
            - hostman-ready # нам нужны на которых hostman-ready=passed
        failed:
            - need_reboot_kernel # и need_reboot_kernel=failed
    restrictions: # фильтруем хосты, на которых стоят запреты на автоматику
        check:
            - automated-reboot
            - reboot
            - automation
    automation: # фильтруем хосты, на которых отключена healing/dns automation
        enabled: true
order: # сортируем полученый результат по hostname
    - hostname
group: # и группируем по локации/стойке (одновременно обрабатываться могут только хосты из одной группы)
    - location
    - rack
postCondition: # условия, которые должны выполниться при завершении таска
    health:
        check: # должны позеленеть эти чеки
            - hostman-ready
            - check_iss_agent
            - need_reboot_kernel
    delay: null
action: reboot # action который применять к хостам (в данном случае будем ребутать хосты)
safetyLevel: NORMAL
ssh: ''
mode: follow # ['follow', 'script'] в script режиме появляется запрет на повторную обработку одного хоста
timeouts: # переопределяем дефолтный cms таймаут
    cms: 7200s
    itdc: null
    default: null
````

*После запуска джобы чтоб спека не потерялась в будущем прикопать
в [specs](https://a.yandex-team.ru/arc_vcs/infra/maxwell/specs)*
