# Быстрые данные для Noapache
**Rearrange Data Fast** – данные для переранжирований верхнего метапоиска (noapacheupper), подгружаемые в рантайме. Обитают в [arcadia/search/web/rearrs_upper/rearrange.fast](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast).

- [Более подробное описание машинерии](how-it-works.md)
- [Как откатить?](rollback.md)
- [Про мониторинги](monitoring.md)
- [Описание алертов](alerts.md)
- [Как чинить?](how-to-fix.md)

{% note alert %}

Ваш код должен быть готов к тому, что данные будут откачены на произвольную предыдущую версию.

{% endnote %}

## Как быстро новые данные доезжают до прода? {#release-speed}
Один полный цикл занимает около 30-45 минут. Из этого:
* 5 минуты на сборку
* 5 минут на аркадийные тесты, 5-6 минут на тестирование с выкладкой на бету и обстрелом
* 15-25 минут на деплой (DL=0.2)

{% note info %}

Графики стадий после переезда на CI стали недоступны. Ожидаем [метрики и статистику от CI](https://st.yandex-team.ru/CI-3810) либо [возможный custom](SEARCH-12048).

{% endnote %}

## На каких вертикалях включено? {#verticals}
* WEB:
    * [CI flow](https://arcanum.yandex-team.ru/projects/noapache-web/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2FWEB&id=fast-data-release)
    * [Мониторинги](https://yasm.yandex-team.ru/panel/fast-data/)
* VIDEO: 
    * [CI flow](https://arcanum.yandex-team.ru/projects/noapache-video/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2FVIDEO&id=fast-data-release)
    * [Мониторинги](https://yasm.yandex-team.ru/panel/fast-data-video/)
* Беты (выкатывается last-released fast-data):
    * [CI flow](https://arcanum.yandex-team.ru/projects/noapache-web/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2Fbetas&id=fast-data-release)
    * [Алертинг](https://juggler.yandex-team.ru/project/report-infra-alerts/aggregate?host=web_sandwich.NOAPACHE_fast_data_age_betas_chart_for_all_dc&service=for_all_dc&project=report-infra-alerts)

{% note warning %}

Шедулеры были отключены после перехода на CI. Ссылки на шедулеры:
* [WEB](https://sandbox.yandex-team.ru/scheduler/17480/view)
* [VIDEO](https://sandbox.yandex-team.ru/scheduler/12405/tasks)
* [Беты](https://sandbox.yandex-team.ru/scheduler/21382/view).

{% endnote %}

## Как попробовать? {#try-it}
{% note tip %}

Минимальный пример: правило FastDataExample:
* [Правило](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/examples/fast_data.cpp)
* [Данные](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast/examples/fast_data)

{% endnote %}

[Описываем структуру](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/examples/fast_data.cpp?rev=3833893#L9-11), в которой храним всё, что душе соблаговолит (далее используется `TFastData` в качестве имени структуры).

### В правиле переранжирования (`T...Rule`) {#rearrange-rule}
1. [Наследуем](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/examples/fast_data.cpp?rev=3833893#L28) правило от `IRearrangeRuleWithFastData<TFastData>`.
2. В конструктор `IRearrangeRuleWithFastData` [передаем относительный путь](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/examples/fast_data.cpp?rev=3833893#L31) до директории правила в [search/web/rearrs_upper/rearrange.fast](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast).
3. [Определяем DoLoadFastData](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/examples/fast_data.cpp?rev=3833893#L40-49) – метод для загрузки данных, вызывается на старте ноапача и при обновлении быстрых данных под ноапачем.
Возвращаем `true`, если данные были успешно загружены и обработаны, и `false`, если нет, в этом случае весь релиз новых данных будет считаться неудачным и данные будут откачены на предыдущую версию (для всех правил и везде).

### В контексте правила (`T...Context`) {#context-rule}
1. [Наследуем](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/examples/fast_data.cpp?rev=3833893#L13) контекст правила от `IFastDataConsumer<TFastData>`.
2. В конструктор `IFastDataConsumer` [передаем экземпляр родительского правила](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/examples/fast_data.cpp?rev=3833893#L16).
3. Через `FastData()` можно получить указатель на структурку. В исключительных случаях указатель может быть равен `nullptr` (например, когда данные не смогли загрузиться на старте noapache), перед разыменованием указателя стоит это учитывать.

## Горячая линия {#hotline}
С вопросами и предложениями в [чат](https://t.me/joinchat/CaUODkNMIpwWNzLu4pngow)!
