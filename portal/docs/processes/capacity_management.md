# Процедура обновления таргетов и алертов

Morda Perl является основным потребителем железа, поэтому оценка ресурсов сейчас проводится именно по ней. В остальные сервисы ресурсы добавляются по необходимости.

### Внести фактические значения
Открыть [эксельку по заказу железа](https://yandexteam.sharepoint.com/:x:/s/morda-dev/EQteH8NpDVpChuZAN0C96CMBfnHsLdRKRHt0vm80vLwqGQ?e=6Shfak).

Внести в эксельку [текущие значения](https://nda.ya.ru/t/Z00MVYla3hidnT) по поверхностям в колонку фактических значений на вкладке Morda Perl (брать графики за месяц, взять максимальное значение).

{% note warning %}

У баннера на НТП иногда меняются адреса: актуальные адреса лежат [в madm](https://madm.yandex-team.ru/edit?export_file=banners_refresh_2&stage=production).
Нужно проверить, что на панельке указаны правильные адреса для графика "НТП Баннер"

{% endnote %}

### Настроить недостающие алерты
В [шаблоне алертов](https://yasm.yandex-team.ru/template/alert/portal.morda.capacity_planning/) добавить новые ручки, имеющие заметный трафик и попадающие под понятие "нужно учитывать ресурсы по ручке".

### Скорректировать имеющиеся алерты
В этом же шаблоне алертов выставить новые значения для rps ручек, которое ожидается к следующему кварталу.
Это нужно, чтобы выдеть рост трафика, выходящий за прогноз.
Для удобства есть [панель алертов](https://yasm.yandex-team.ru/template/panel/capacity_planning_alerts/), построенная по этому шаблону алертов.

### Оценить рост трафика и времени ответа
Если это случилось, то это означает перерасход плана по железу. Нужно выяснить, почему увеличился трафик, увеличилось время ответа, и предпринять меры.

### Выставить новые таргеты учений
Для таргетов расчитываются значения по уровню трафика, который ожидается в следующем квартале. Если на текущих учениях прогнозируемый таргет получить не удаётся, это повод предпринять меры.

Формула коэффициента запаса описана [тут](https://docs.yandex-team.ru/portal/processes/hardware_order#kak-schitaetsya-koefficient-zapasa).

Примеры расчетов для предыдущих периодов есть в эксельке.

Таргеты выставляются в [интерфейсе учений](https://uchenki.yandex-team.ru/settings/service).

# Мониторинг трафика на морду по продуктам

## Панельки

* [capacity.products](https://yasm.yandex-team.ru/template/panel/capacity.products/) - трафик по продуктам + время ответа
* [capacity.sources](https://yasm.yandex-team.ru/template/panel/capacity.sources/prj=portal-morda/) - трафик по источникам + время ответа
* [capacity_planning_alerts](https://yasm.yandex-team.ru/template/panel/capacity_planning_alerts/) - панелька алертов, которые заводятся в шаблоне алертов (ссылка ниже)

## Алерты

* [portal.morda.capacity_planning](https://yasm.yandex-team.ru/template/alert/portal.morda.capacity_planning/) - алерты для мониторинга трафика и времени ответа

## Оповещения

* [Morda Capacity Planning](https://t.me/+b4DajW_--no2YjE6) - чат, куда приходят оповещения по трафику и времени ответа (настраиваются в шаблоне алертов, ссылка на который выше)

## Репозиторий

Все шаблоны панелей и алертов коммитятся в [репозиторий](https://a.yandex-team.ru/arc/trunk/arcadia/portal/devops/monitoring).
