#### Причины отклонения фидбека

При отклонении фидбека в НК его надо отклонять с конкретной причиной, почему он отклонён. Список допустимых причин в [схеме](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/schemas/social/social.feedback.schema.json). Причины отклонения могут быть автоматическими и не видны из ui, могут различаться для фидбека и гипотез. Кроме отклонения фидбека используются для перенаправления в другие сервисы, наример Справочник/Саппорт/Трекер. Допустимые причины отклонения [вычисляются](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/social/feedback/agent.cpp?rev=r9380314#L323) в зависимости от источника (source) фидбэка.

#### Как добавить новую причину отклонения

Пример [ревью](https://a.yandex-team.ru/review/2480152/details) с добавлением новой причины в НК.

1. Добавить значение в бд, [как здесь](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/migrations/migrations/V543__NONTRANSACTIONAL_new_auto_clean_web_reject_reason.sql?rev=r9375546#L1)
2. Поправить [json-схему](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/schemas/social/social.feedback.schema.json?rev=r9452196#L16).
3. Добавить это же значение в модель данных, [хедер](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/social/include/yandex/maps/wiki/social/feedback/enums.h?rev=r9375546#L40), [cpp](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/social/feedback/enums.cpp?rev=r9375546#L38).
4. Проверить и, возможно, обновить [списки](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/social/feedback/agent.cpp?rev=r9380314#L323) валидных причин отклонения для разных флоу обработки фидбека.
5. Если причина отклонения используется для пользовательского фидбека, т.е. прорастает в [fbapi](https://docs.yandex-team.ru/maps-feedback/):
   1. Надо добавить её в http-клиент fbapi: [хедер](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/http/include/yandex/maps/wiki/http/fbapi/models/common.h?rev=r9375546#L30), [cpp](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/http/fbapi/models/common.cpp?rev=r9375546#L27)
   2. Поддержать новую причину в fbapi, [пример](https://a.yandex-team.ru/review/2507248/files/1#file-0-173650696).
   3. Настроить соответствие причин отклонения в НК и fbapi, [код](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_feedback/src/sync_fbapi_feedback_worker/lib/fbapi_update_extra_data.cpp?rev=r9375546#L16)
   4. Протащить новую причину в статистику, [инструкция](https://docs.yandex-team.ru/maps-feedback/stat/fbapi_metrics#add-reject-reason).
6. Добавить ключи в [танкер](https://tanker.yandex-team.ru/project/nmaps/keyset/feedback?branch=master&statuses=*%3D&search=reject-reason) аналогично остальным причинам отклонения для отображения в НК.
7. Если причину отклонения нужно выбирать в ui НК, надо добавить её в метаинформацию про причины [хедер](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/social/src/libs/feedback-actions/meta.h?rev=r9323664#L12). Эта метаинформация задаёт расположение причины в карточке фидбэка.

###### Порядок выкатки сервисов:
1. Выкатить поддержку новой причины отклонения в fbapi
2. Убедиться, что в танкере готовы переводы новых ключей
3. Выкатить сервисы НК
3. Дождаться, когда в проде появится фидбек, отклонённый с новой причиной
4. Поправить [статистику](https://docs.yandex-team.ru/maps-feedback/stat/fbapi_metrics#add-reject-reason)
