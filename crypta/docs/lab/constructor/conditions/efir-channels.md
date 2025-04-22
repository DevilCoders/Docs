Каналы на Я.Эфире
=====================

Этот тип правила позволяет найти тех, кто смотрел видео с перечисленных каналов Эфира.

Чтобы определить идентификатор канала Эфира, можно воспользоваться [страницей видео статистики](https://stat.yandex-team.ru/Video/Others/Strm/strm_cube_2?scale=d&os_family=_total_&browser=_total_&ref_from=_total_&provider=_total_&view_type=_total_&channel=_total_&program=_total_&country=_total_&_incl_fields=microsessions_with_view&sort_field=_TOTALS_%5Emicrosessions_with_view&sort_reverse=1&date_min=2020-03-01+00%3A00%3A00&date_max=2020-03-12+23%3A59%3A59). Нужно выбрать поле *Канал* и ввести часть названия.

{% note warning %}

Обращайте внимание на наличие и количество пробелов в названиях.

{% endnote %}

**Пример**: хотим собрать сегмент пользователей, которые смотрели Дудя в Эфире.
Для вДудь существует несколько идентификаторов канала, отвечающих за разные источники видео. Если нам нужно найти всех, кто смотрел видео, вне зависимости от источника, в сегменте указываем все три наименования.

![efir-video-users-screenshot](https://wiki.yandex-team.ru/crypta/crypta-up/lab/constructor/.files/screenshot2020-04-22at1.22.21pm.png)

Правило тогда будет выглядеть вот так:

<img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-05-14%20at%204.31.39%20PM.png" alt="drawing" style="width:500px;"/>

Если идентификаторов каналов слишком много, как, например, для НХЛ, а мы хотим собрать аудиторию со всех, можно взять только часть названия, общую для всех каналов.

На скриншоте видно, что *НХЛ* есть во всех названиях, при этом не нашлось никаких лишних каналов.

![efir-video-nhl-screenshot](https://wiki.yandex-team.ru/crypta/crypta-up/lab/constructor/.files/screenshot2020-04-22at1.31.11pm.png)

Тогда в можно сделать вот такое правило:

<img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-05-14%20at%204.31.58%20PM.png" alt="drawing" style="width:500px;"/>

Этот тип правила требует подтверждения. После создания нужно нажать *Отправить на проверку*. 
