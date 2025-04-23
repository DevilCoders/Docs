## DeleteUnusedHyperGeosJob

### Продукт/подсистема

Удаление неиспользуемых гипер гео (условий ретаргетинга с retargeting_conditions_type = geo_segments)
и сегментов (записей в hypergeo_segments и самих сегментов в Яндекс.Аудитории).


### Роль в работе продукта/подсистемы

Удаляет неиспользуемые в группах и неудалившиеся автоматически (например, из-за ошибки при сохранении группы) гипер гео и сегменты.
Я.Аудитории имеют ограничение на число неиспользующихся сегментов, поэтому если их не удалять, то пользователь перестанет иметь возможность их создавать
(сейчас новые сегменты автоматически создаются при использовании гиперлокала - Точного местоположения в Регионах показа группы).


### Датафлоу

- Читает список неудаленных неиспользумых гипер гео (нет связанной записи в таблице [ppc.adgroups_hypergeo_retargetings](https://direct-dev.yandex-team.ru/db/ppc/tables/adgroups_hypergeo_retargetings.html)) из таблицы [ppc.retargeting_conditions](https://direct-dev.yandex-team.ru/db/ppc/tables/retargeting_conditions.html);
- Удаляет неиспользуемые гипер гео (проставляет is_deleted = 1 и очищает остальные поля в таблице [ppc.retargeting_conditions](https://direct-dev.yandex-team.ru/db/ppc/tables/retargeting_conditions.html); удаляет связанные цели в таблице [ppc.retargeting_goals](https://direct-dev.yandex-team.ru/db/ppc/tables/retargeting_goals.html));
- Читает сегменты, связанные с удаленными на предыдущем шаге гипер гео, и удаляет неиспользуемые (не используются в качестве goal_id в [retargeting_goals](https://direct-dev.yandex-team.ru/db/ppc/tables/retargeting_goals.html)) из таблицы [hypergeo_segments](https://direct-dev.yandex-team.ru/db/ppc/tables/hypergeo_segments.html);
- Читает все остальные сегменты, несвязанные ни с каким гипер гео, и удаляет их из таблицы [hypergeo_segments](https://direct-dev.yandex-team.ru/db/ppc/tables/hypergeo_segments.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.DeleteUnusedHyperGeosJob.working.production&query=&last=3DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'hypergeo.DeleteUnusedHyperGeosJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Перестанут удаляться неиспользуемые гипер гео и сегменты Я.Аудиторий.
Из-за этого через какое-то время может перестать работать сохранение групп с гиперлокалом для тех пользователей,
кто превысит лимит Я.Аудиторий на число неиспользуемых сегментов.


### Как пользователи (или команда) заметят проблему и через какое время

Некоторые пользователи начнут получать ошибку при попытке сохранить группу с гиперлокалом. [Пример тикета](https://st.yandex-team.ru/DIRECT-162899).

Число неиспользуемых неудаленных гипер гео проверяется [запросом](https://yql.yandex-team.ru/Operations/Yl13QVZ1Ow7cPMG4RQ17lNlUiws9Ep7DjNzBZSHrxZA=).

Число неиспользуемых сегментов - [запросом](https://yql.yandex-team.ru/Operations/Yl13PlZ1Ow7cPMGzEeMN7lN-r-zjnTkXDB_lfiUJoXE=).


### Контакты разработчиков и менеджеров

Разработчики: [Дмитрий Лянге](https://staff.yandex-team.ru/dlyange) <br/>
Менеджеры: [Дмитрий Субботин](https://staff.yandex-team.ru/saturday), [Павел Катайкин](https://staff.yandex-team.ru/pavelkataykin)


### Желательное время исправления в случае поломки

В течение недели. Проблемы могут возникнуть из-за большого числа неудаленных сегментов в Я.Аудиториях;
на момент написания число таких сегментов увеличивается со скоростью [<200 в день](https://st.yandex-team.ru/DIRECT-162907#625e5892814a1b71566a4d39).

Есть ваншот [DeleteUnusedHyperGeosOneshot](https://a.yandex-team.ru/arc_vcs/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/hypergeo/DeleteUnusedHyperGeosOneshot.kt),
через который можно сделать те же операции.

До написания ваншота и джобы проблема лечилась рекомендацией пользователям вручную удалить неиспользуемые сегменты в Я.Аудиториях.


### Способы регулирования работы джобы

PpcProperty hyper_geo_ids_to_delete_limit хранит лимит числа удаляемых объектов гипер гео и сегментов.
При отсутствии значения у этого проперти используется дефолтное значение в 4_000.

PpcProperty hyper_geo_segment_ids_to_bypass_deleting хранит id гео сегментов, которые не нужно пытаться удалять.
Например, используется для сегментов, на которые пользователи сами завязали lal-ы, и теперь их удалить из Аудиторий не выйдет, хотя в Директе эти сегменты больше не используются.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

- Сегменты Я.Аудиторий могут перестать удаляться, если протухнет токен Я.Аудиторий (в логах появятся ошибки ru.yandex.direct.audience.client.exception.YaAudienceClientTypedException: Invalid oauth_token).
Сама джоба продолжит успешно отрабатывать и удалять только гипер гео.
После обновления токена в oneshot все неудаленные за этот период сегменты будут удалены при следующем запуске джобы.
[Тикет на обновление токена](https://st.yandex-team.ru/DIRECT-167456).


- Не все сегменты Я.Аудиторий (и связанные с ними записи в таблице [hypergeo_segments](https://direct-dev.yandex-team.ru/db/ppc/tables/hypergeo_segments.html)) могут быть успешно удалены.
Для таких сегментов Я.Аудитории возвращает ошибку (ru.yandex.direct.audience.client.exception.YaAudienceClientTypedException: Access is denied),
и ожидается, что джоба будет безуспешно пытаться их удалить каждый день, пока они не будут добавлены в проперти hyper_geo_segment_ids_to_bypass_deleting. Порядок числа таких сегментов - несколько десятков.
Пример такого поведения: [в логах работы джобы](https://direct.yandex.ru/logviewer/short/iSqxNO_053E74h).
[Объяснение](https://st.yandex-team.ru/DIRECT-167086#625d549c7573366160a1db7b).
