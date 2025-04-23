# Пятничные хлопанья

## Что это
**Процедура тренировки по пятницам поочередного закрытия локаций (ДЦ) и тренировки оповещения команд.**

## Зачем
Во время пятничных учений проверяется:
* готовность и исправность инструментов управления балансировкой трафика для экстренной перебалансировке трафика из одного ДЦ в оставшиеся;
* способность сервисов\компонентов\вертикалей переживать резкие перепады трафика, неизбежные при экстренном снятии трафика с одного из датацентров, без выхода за установленные компонентом или сервисом KPI метрики;

## Как происходит
Марти поочередно закрывает датацентры SAS, MAN, VLA, отслеживая состояние метрик мониторинга.

## Важно
* Не должно быть блокеров (сверхсрочные релизы или аварийные ситуации);
* Блокируются за час до начала плановые релизы, при вопросах от команд про выкатки релизов с их стороны самостоятельно толькоп при условии, что команда успеет до начала хлопаний, иначе просим перенести старт выкатки на время после хлопаний;
* Изменить очередность ДЦ, перенести или отменить учения могут только @bunnyhop или @dmitryno;
* Перед учениями необходимо убедиться в наличии события в календаре блокирующих работ (красный календарь).
* В случае отсутствия - обратиться к ответственным из [сервиса Ученек](https://warden.yandex-team.ru/components/spi-tools/s/uchenki);
* Раз в две недели проводится со снятием L3 анонса на ДЦ (обозначается дополнительным событием в календаре во время ученек).
* Возможные отступления от данной процедуры (включая изменения в последовательности закрытия локаций) должны быть согласованы с @bunnyhop или @dmitryno.

## Последовательность

{% list tabs %}
- С L3
    Галочка | Минут от начала | Время | Действие
    --: | ---: | ---: | :---
    <input type="checkbox" /> | -60 | 16:20 | Фриз релизов в [rviewer](https://rviewer.yandex-team.ru/schedule)
    <input type="checkbox" /> | -15 | 17:05 | Бот должен написать в чат ученек ([если бот не написал](#YaIncBot-crash))
    <input type="checkbox" /> | -5 | 17:15 | Марти в чат ученек: `Начинаем через 5 минут, нет возражений?`
    <input type="checkbox" /> | 0 | 17:20 | Марти в чат ученек: `Начинаем c SAS, закрываем на L7`
    <input type="checkbox" /> | 0 | 17:20 | Марти выставляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в SAS
    <input type="checkbox" /> | 0 | 17:20 | Марти закрывает SAS [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 3 | 17:23 | Марти в чат ученек: `Снимаем сервисные в SAS`
    <input type="checkbox" /> | 3 | 17:23 | Марти снимает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/sas) в SAS
    <input type="checkbox" /> | 6 | 17:26 | Марти в чат ученек: `Снимаем анонс с L7 SAS`
    <input type="checkbox" /> | 6 | 17:26 | Марти [cнимает анонс с L7 в SAS](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 9 | 17:29 | Марти в чат ученек: `Возвращаем анонс L7 SAS`
    <input type="checkbox" /> | 9 | 17:29 | Марти [возвращает анонс с L7 в SAS](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 12 | 17:32 | Марти в чат ученек: `Возвращаем сервисные в SAS`
    <input type="checkbox" /> | 12 | 17:32 | Марти возвращает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/sas) в SAS
    <input type="checkbox" /> | 15 | 17:35 | Марти в чат ученек: `Открываем SAS`
    <input type="checkbox" /> | 15 | 17:35 | Марти открывает SAS [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 17 | 17:37 | Марти удаляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в SAS
    <input type="checkbox" /> | 18 | 17:38 | Марти в чат ученек: `SAS открыт, переходим к закрытию MAN`
    <input type="checkbox" /> | 18 | 17:38 | Марти выставляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в MAN
    <input type="checkbox" /> | 18 | 17:38 | Марти закрывает MAN [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 21 | 17:41 | Марти в чат ученек: `Снимаем сервисные в MAN`
    <input type="checkbox" /> | 21 | 17:41 | Марти снимает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/man) в MAN
    <input type="checkbox" /> | 24 | 17:44 | Марти в чат ученек: `Снимаем анонс с L7 MAN`
    <input type="checkbox" /> | 24 | 17:44 | Марти [cнимает анонс с L7 в MAN](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 27 | 17:47 | Марти в чат ученек: `Возвращаем анонс с L7 MAN`
    <input type="checkbox" /> | 27 | 17:47 | Марти [возвращает анонс с L7 в MAN](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 30 | 17:50 | Марти в чат ученек: `Возвращаем сервисные в MAN`
    <input type="checkbox" /> | 30 | 17:50 | Марти возвращает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/man) в MAN
    <input type="checkbox" /> | 33 | 17:53 | Марти в чат ученек: `Открываем MAN`
    <input type="checkbox" /> | 33 | 17:53 | Марти открывает MAN [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 35 | 17:55 | Марти удаляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в MAN
    <input type="checkbox" /> | 36 | 17:56 | Марти в чат ученек: `MAN открыта, переходим к закрытию VLA`
    <input type="checkbox" /> | 36 | 17:56 | Марти выставляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в VLA
    <input type="checkbox" /> | 36 | 17:56 | Марти закрывает VLA [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 37 | 17:57 | Отредактировать событие в infra, т.к. окончание хлопаний будет позже 18:00
    <input type="checkbox" /> | 39 | 17:59 | Марти в чат ученек: `Снимаем сервисные в VLA`
    <input type="checkbox" /> | 39 | 17:59 | Марти снимает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/vla) в VLA
    <input type="checkbox" /> | 42 | 18:02 | Марти в чат ученек: `Снимаем анонс с L7 VLA`
    <input type="checkbox" /> | 45 | 18:05 | Марти [возвращает анонс с L7 в MAN](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 48 | 18:08 | Марти в чат ученек: `Возвращаем сервисные в VLA`
    <input type="checkbox" /> | 48 | 18:08 | Марти возвращает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/vla) в VLA
    <input type="checkbox" /> | 53 | 18:11 | Марти в чат ученек: `Открываем VLA`
    <input type="checkbox" /> | 53 | 18:11 | Марти открывает VLA [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 55 | 18:13 | Марти удаляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в VLA
    <input type="checkbox" /> | 56 | 18:14 | Марти  в чат ученек: `/uchenki finish closing`
- Без L3
    Галочка | Минут от начала | Время | Действие
    --: | --: | ---: | :---
    <input type="checkbox" /> | -60 | 16:20 | Фриз релизов в [rviewer](https://rviewer.yandex-team.ru/schedule)
    <input type="checkbox" /> |-15 | 17:05 | Бот должен написать в чат ученек ([если бот не написал](#YaIncBot-crash))
    <input type="checkbox" /> | -5 | 17:15 | Марти в чат ученек: `Начинаем через 5 минут, нет возражений?`
    <input type="checkbox" /> | 0 | 17:20 | Марти в чат ученек: `Начинаем c SAS, закрываем на L7`
    <input type="checkbox" /> | 0 | 17:20 | Марти выставляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в SAS
    <input type="checkbox" /> | 0 | 17:20 | Марти закрывает SAS [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 3 | 17:23 | Марти в чат ученек: `Снимаем сервисные в SAS`
    <input type="checkbox" /> | 3 | 17:23 | Марти снимает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/sas) в SAS
    <input type="checkbox" /> | 6 | 17:26 | Марти в чат ученек: `Возвращаем сервисные в SAS`
    <input type="checkbox" /> | 6 | 17:26 | Марти возвращает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/sas) в SAS
    <input type="checkbox" /> | 9 | 17:29 | Марти в чат ученек: `Открываем SAS`
    <input type="checkbox" /> | 9 | 17:29 | Марти открывает SAS [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 11 | 17:31 | Марти удаляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в SAS
    <input type="checkbox" /> | 12 | 17:32 | Марти в чат ученек: `SAS открыт, переходим к закрытию MAN`
    <input type="checkbox" /> | 12 | 17:32 | Марти выставляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в MAN
    <input type="checkbox" /> | 12 | 17:32 | Марти закрывает MAN [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 15 | 17:35 | Марти в чат ученек: `Снимаем сервисные в MAN`
    <input type="checkbox" /> | 15 | 17:35 | Марти снимает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/man) в MAN
    <input type="checkbox" /> | 18 | 17:38 | Марти в чат ученек: `Возвращаем сервисные в MAN`
    <input type="checkbox" /> | 18 | 17:38 | Марти возвращает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/man) в MAN
    <input type="checkbox" /> | 21 | 17:41 | Марти в чат ученек: `Открываем MAN`
    <input type="checkbox" /> | 21 | 17:41 | Марти открывает MAN [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 23 | 17:43 | Марти удаляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в MAN
    <input type="checkbox" /> | 24 | 17:44 | Марти в чат ученек: `MAN открыта, переходим к закрытию VLA`
    <input type="checkbox" /> | 24 | 17:44 | Марти выставляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в VLA
    <input type="checkbox" /> | 24 | 17:44 | Марти закрывает VLA [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 27 | 17:47 | Марти в чат ученек: `Снимаем сервисные в VLA`
    <input type="checkbox" /> | 27 | 17:47 | Марти снимает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/vla) в VLA
    <input type="checkbox" /> | 30 | 17:50 | Марти в чат ученек: `Возвращаем сервисные в VLA`
    <input type="checkbox" /> | 30 | 17:50 | Марти возвращает [анонс сервисных балансеров](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/vla) в VLA
    <input type="checkbox" /> | 33 | 17:53 | Марти в чат ученек: `Открываем VLA`
    <input type="checkbox" /> | 33 | 17:53 | Марти открывает VLA [bulk'ом](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common)
    <input type="checkbox" /> | 35 | 17:55 | Марти удаляет [downtime](https://juggler.yandex-team.ru/dashboards/downtimer/) в VLA
    <input type="checkbox" /> | 36 | 17:56 | Марти  в чат ученек: `/uchenki finish closing`
{% endlist %}

{% note info "Примечание" %}

{#YaIncBot-crash}

В случае сбоя оповещения в [чате](https://t.me/joinchat/RwmSLjQAGzFkYjAy) [сервиса Ученек](https://warden.yandex-team.ru/components/spi-tools/s/uchenki):

* Зафиксировать инцидент в SPI для разбора дежурными [сервиса Ученек](https://warden.yandex-team.ru/components/spi-tools/s/uchenki).
* Сделать `/martycast` через YaIncBot со следующим текстом:
    * При начале работ
        ```
        Через 15 минут начинаем проверку аварийного закрытия локаций.
        Последовательность: SAS, MAN, VLA.
        Просим дежурных девопсов сервисов под L7 быть на связи, перекличка не требуется.
        Дежурные сервисов не под L7, будьте готовы к повышенной нагрузке от соседей.
        Координация в чате https://t.me/joinchat/RwmSLjQAGzFkYjAy
        ```
    * По окончании работ
        ```
        Учения завершены
        ```
{% endnote %}

## HowTo

### Закрытие и открытие через bulk
Это перераспределение трафика между локациями на уровне L7 балансеров через [bulk actions в секции common L7-heavy в Няне](https://nanny.yandex-team.ru/ui/#/list-l7heavy/common).

![](https://jing.yandex-team.ru/files/lensws/2021-11-22_22-07-33.png)
* через выставление нулевого веса для закрываемой локации
    * Делается через "Close using default weights"
* через возвращения значения по умолчанию (33 или 34) при открытии назад закрытой локации
    * Делается через "Reset to default weights"

![](https://jing.yandex-team.ru/files/lensws/2021-11-22_22-07-53.png)

### Сервисные балансеры
Cнятие\возвращение анонса сервисных балансеров [на странице управления сервисными балансерами в Няне](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/).

{% note warning %}

Сперва необходимо выбрать **нужную локацию!**, следует обратить внимание что **список ДЦ идет по алфавиту**, далее `Apply all` для выключения анонса сервисных, `Cancel all` для включения.
![](https://jing.yandex-team.ru/files/lensws/2021-11-22_22-03-50.png)

{% endnote %}

### Cнятие L3 анонса на датацентр
Раз в две недели проводится снятие терм-слоя L7 вместе со снятием L3 анонса на ДЦ (обозначается дополнительным событием в календаре во время ученек). Дежурный марти меняет поведение терм-слоя L7 [в интерфейсе l7_heavy в ITS](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/). Терм-слой L7 переключает healthcheck коды ответа (с 200 на 503) на проверки L3.

{% note warning %}

Необходимо использовать секции локаций ДЦ без `_only` постфикса, режим включенного состояния - выбирайте с `return_200__weighted`, а режим отключенного `return_503`
![](https://jing.yandex-team.ru/files/lensws/2021-11-22_21-42-34.png)

{% endnote %}
