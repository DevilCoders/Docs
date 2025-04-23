[О мониторингах джоб](../../concepts/dev/jobs-monitoring.md) <br/>

## Как настроить событийный мониторинг джобы { #onejob }

В данном руководстве механика работы Juggler (системы событийного мониторинга) будет описываться в упрощенной форме. За более подробной информацией обращайтесь к [документации Juggler](https://docs.yandex-team.ru/juggler/).

{% note info %}

На данный момент руководство содержит шаги для настройки мониторинга внутри команды. Настройка мониторинга для передачи в app-duty появится в скором времени.

{% endnote %}

{% note info %}

Если после прочтения доки у вас останутся вопросы, не стесняйтесь спрашивать у [знающих людей](../../reference/who-knows#ops-monitorings).

{% endnote %}

### 1. Добавьте аннотацию JugglerCheck { #onejob-jugglercheck }

Можно добавить несколько аннотаций, если требуются разные настройки мониторинга в разных окружениях.

Пример:
```java
@JugglerCheck(needCheck = ProductionOnly.class,
        ttl = @JugglerCheck.Duration(hours = 1),
        tags = {DIRECT_API_TEAM},
        urls = {
            @Url(title = "Возраст очереди в часах", url = "https://solomon.yandex-team.ru/..."),
        },
        notifications = @OnChangeNotification(
                method = NotificationMethod.TELEGRAM,
                recipient = NotificationRecipient.CHAT_API_MONITORING,
                status = {JugglerStatus.OK, JugglerStatus.CRIT}
        )
)
```
В этом примере мониторинг настроен следующим образом: если в течение часа в продакшене джобе не удастся хотя бы один раз успешно отработать, то в telegram-чат будет отправлена нотификация; так же будет отправлена нотификация, когда джоба снова заработает.

Параметры:

- `needCheck` - задает условие, при котором применяется аннотация ([подробнее](#onejob-needcheck)).
- `ttl` - задает период, за который джоба должна хотя бы один раз успешно отработать ([подробнее](#onejob-ttl)).
- `tags` - теги, которыми помечаются события, которые джоба отправляет в [Juggler](https://docs.yandex-team.ru/juggler/). На основе тегов можно настраивать нотификации в самом Juggler. Так же используется для разметки самих джоб ([подробнее](#onejob-tags)).
- `urls` - список ссылок, которые будут видны в веб-интерфейсе Juggler.
- `notifications` - список нотификаций.

Параметры нотификации:
- `method` - способ нотифицирования (телеграм, почта и пр.) ([подробнее](#onejob-notifications-method)).
- `recipient` - получатель нотификации ([подробнее](#onejob-notifications-recipient)).
- `status` - список статусов, при переключении в которые будет отправлена нотификация ([подробнее](#onejob-notifications-status)).


### 2. Настройте условие проверки { #onejob-needcheck }

Наличие у джобы хотя бы одной аннотации JugglerCheck для продакшен-окружения является обязательным.

Если описываемая проверка требуется только в продакшене, укажите [ProductionOnly](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/java/ru/yandex/direct/env/ProductionOnly.java).

Так же вам могут пригодиться [TypicalEnvironment](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/java/ru/yandex/direct/env/TypicalEnvironment.java), [NonProductionEnvironment](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/java/ru/yandex/direct/env/NonProductionEnvironment.java) и другие реализации [EnvironmentCondition](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/java/ru/yandex/direct/env/EnvironmentCondition.java).


### 3. Настройте период проверки { #onejob-ttl }

Если в течение указанного периода джоба ни разу не отработала успешно, то проверка джобы ("агрегат" в Juggler) получит статус "CRIT", и будут отправлены нотификации по правилам, описанным в поле `notifications`. Если же в течение указанного периода джоба хотя бы один раз успешно отработала (отправила в Juggler статус "OK"), то проверка получит статус "OK" и нотификации не будут отправлены.

Таким образом, период должен быть подобран исходя из нескольких соображений:

- Он должен быть устойчив к случайным ошибкам в работе джобы, которые не приводят к отказу функциональности. Например, джоба упала из-за недоступности сети, а при следующем запуске успешно отработала, и при этом пользователи не могли заметить перебой. В этом случае получать нотификацию будет избыточным, такие нотификации называют "шумом".
- Если поломка джобы приводит к заметным функциональным проблемам (например, заметным для пользователей), то проверка должна получать статус "CRIT".

**Рекомендуемый период проверки - примерно 2.5 - 3.5 периодов работы джобы.** Например, если джоба запускается раз в 30 минут, то скорее всего никто не заметит, если она не будет работать полтора часа. Если же поставить период меньше, скажем, 40 минут, тогда с большой вероятностью мониторинг будет "моргать" при мигании сети, таймауте запроса во внешний сервис и т.п., то есть "создавать шум" и отвлекать от реальных проблем.


### 4. Установите теги { #onejob-tags }

Установите тег своей группы (например `CheckTag.GROUP_INTERNAL_SYSTEMS`).
Если джоба обращается к YT, установите тег `CheckTag.YT`.
Если это очень важная джоба, стоит подумать о добавлении тега `CheckTag.JOBS_RELEASE_REGRESSION` ([javadoc](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/juggler-check/src/main/java/ru/yandex/direct/juggler/check/model/CheckTag.java)) - посоветуйтесь об этом с [@ppalex](https://staff.yandex-team.ru/ppalex).

{% note info "Агрегаты для нескольких джоб" %}

Для каждого тега в Juggler собирается отдельный агрегат, который включает в себя агрегаты всех джоб, размеченных этим тегом. Подробнее [о верхнеуровных агрегатах](#jobgroup).

{% endnote %}


### 5. Добавьте полезные ссылки { #onejob-links }

В аннотации можно указать дополнительные ссылки в поле `urls` (см. [пример выше](#onejob-jugglercheck)). Они будут отображаться в веб-интерфейсе Juggler в агрегате для джобы. Это могут быть, например, графики.

![Ссылки в интерфейсе Juggler](_assets/juggler-links.png "Ссылки в интерфейсе Juggler" =649x85)

{% note info "Автогенерация ссылок" %}

В агрегате появятся автосгенерированные ссылки на логи джобы в LogViewer, документацию в docs и код в Аркануме. Добавлять их вручную не нужно!

{% endnote %}


### 6. Настройте нотификации { #onejob-notifications }

Добавьте одно или несколько правил нотификаций.


#### 6.1. Выберите способ нотифицирования { #onejob-notifications-method}

[Доступные способы нотифицирования](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/ansible-juggler/src/main/java/ru/yandex/direct/ansiblejuggler/model/notifications/NotificationMethod.java). Самым популярным способом является Telegram.


#### 6.2. Укажите получателя { #onejob-notifications-recipient }

В качестве полчателя для нотификаций типа email укажите логин(ы) на staff'е.

Нотификации в Telegram можно получать в личку и в чаты.

Чтобы впервые начать получать нотификации на определенный логин или в чат в Telegram, потребуется предварительная настройка ([инструкция](https://docs.yandex-team.ru/juggler/notifications/on_change#telegram)). После её прохождения добавьте логин или название чата в [NotificationRecepient](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/juggler-check/src/main/java/ru/yandex/direct/juggler/check/model/NotificationRecipient.java).

После этого можно использовать новое значение `NotificationRecepient` для нотификаций в телеграм.


#### 6.3. Укажите список статусов { #onejob-notifications-status }

Каждый статус в списке означает, что нотификация будет отправляться, когда проверка будет переходить из любого другого статуса в указанный. Например, если указать только `JugglerStatus.CRIT`, то нотификация будет отправлена при переходе статуса из `ok` в `crit`, но не в обратную сторону. Поэтому, обычно в этом поле указываются два статуса: `{JugglerStatus.OK, JugglerStatus.CRIT}`.

{% note tip "Вы можете управлять состоянием джобы с помощью явной установки статуса" %}

Помимо генерации исключения, можно явно выставить статус джобы с помощью метода базового класса `BaseDirectJob.setJugglerStatus`, который так же принимает описание проблемы. Будьте внимательны: если джоба всего раз сообщит об ошибке за указанный ttl, а отработает несколько раз, то проверка не изменит статус. Не забудьте записать детали проблемы в error-log.

{% endnote %}


## Как найти агрегат (проверку, лампочку) для джобы, созданный в джагглере из аннотации { #find-aggr }

- Зайдите в интерфейс [Juggler](https://juggler.yandex-team.ru).
- Перейдите на вкладку "Aggregates".
- Введите в поисковую строку `service=jobs.<Название джобы>.working.<название окружения>`. Например: `service=jobs.AggregatedStatusesProcessor.working.production`.
- В результах поиске вы увидите проверку, созданную автоматически по аннотации. Перейдите в неё, чтобы посмотреть историю и настройки.

{% note info "Когда создаётся агрегат?" %}

Для каждого типа окружения агрегаты создаются запущенным приложением jobs для этого типа окружения. В тестинге агрегаты появляются после выкладки нового релиза на ТС, а в продакшене - после выкладки его в продакшен. Обновление агрегатов происходит раз в пол часа.

{% endnote %}

{% note info "Дополнительные ссылки в Juggler-агрегате" %}

В собранном агрегате справа вверху появятся автосгенерированные ссылки на логи, документацию в docs и код в Аркануме. Так же можно вручную добавить дополнительные ссылки через аннотацию ([подробнее](#onejob-links)).

{% endnote %}


## Как настроить агрегирующий мониторинг группы джоб { #jobgroup }

Бывает полезно иметь в Juggler единый агрегат (лампочку) по группе джоб, объединенных некоторым признаком - тегом. Эта лампочка будет загораться, если загорелась хотя бы одна лампочка по джобе, входящей в группу. Например, все джобы, имеющие приоритет критичности `PRIORITY_0` размечены тегом `CheckTag.DIRECT_PRIORITY_0`. По ним собираются агрегаты для нескольких сред: [jobs.toplevel_direct_priority_0.working.production](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.toplevel_direct_priority_0.working.production&query=&last=1DAY), [jobs.toplevel_direct_priority_0.working.test](https://juggler.yandex-team.ru/check_details/?host=direct.checks.test&service=jobs.toplevel_direct_priority_0.working.test&query=&last=1DAY).

Чтобы в Juggler создать такой верхнеуровневый агрегат:
1. Проверьте, нет ли уже в enum [CheckTag](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/juggler-check/src/main/java/ru/yandex/direct/juggler/check/model/CheckTag.java) подходящего тега.
2. Если тега нет, добавьте его и сопроводите javadoc.
3. Проставьте тег в аннотации `JugglerCheck` всех объединяемых джобах. Типы окружений, для которых будут созданы агрегаты, определяются условием в `needCheck`.

Чтобы найти агрегат по группе джоб, воспользуйтесь [инструкцией выше](#find-aggr), но для поиска используйте строку формата `service=jobs.toplevel_<имя тега из CheckTag(то что из строкового параметра)>.working.<тип окружения>`.

{% note warning "Особый смысл тегов DIRECT_PRIORITY_<N>" %}

Агрегаты, собранные по этим тегам, отображаются на дэшборде дежурных app-duty. Эти теги выставляются только при передаче джоб в централизованный мониторинг app-duty (см. [Централизованный мониторинг в рамках дежурства app-duty](../../concepts/dev/jobs-monitoring.md#stages-appduty)).

{% endnote %}
