# Сигналы для мониторинга клиентов логброкера

## Сигналы хендлеров

Отгружаем через пуш-схему Хунистатера.

Сигналы по числу записей:
```
<имя брокера>.entries.total.<путь к логу>_dmmm
<имя брокера>.entries.<сервер>.<путь к логу>_dmmm
```

Если вместо сервера указан total, то сигнал содержит сигнал по логу, без учета сервера.

Имя сервера и путь к логу присылает логброкер.

## Имена метрик:

* events — число событий в сообщениях из логбровкера

## Метрики из passport_grpahite.log

Считаем статусы походов во внешние сервисы по графитному логу билдеров.

```
graphite_log.builder.rps.total.<service>_dmmm — все обращения в сервис
graphite_log.builder.rps.success.<service>_dmmm — удачные обращения в сервис
graphite_log.builder.rps.failed.<service>_dmmm — неудачные образения (failed или timeout)
```

## Настройки Хунистатера:

| Имя брокера | Порт Хунистатера | Порт внутренних метрик Хунистатера | itype | prj |
| ----------- | ---------------- | ---------------------------------- | ----- | --- |
| account_events | 10291 | 10391 | passportlbcae | logbroker-client-account-events |
| avatars | 10301 | 10401 | passportlbavatars | logbroker-client-avatars |
| historydb | 10292 | 10392 | passportlbchdb | logbroker-client-historydb |
| historydb_yt | 10303 | 10403 | passportlbchdbyt | logbroker-client-historydb-yt |
| oauth | 10293 | 10393 | passportlbcoauth | logbroker-client-oauth |
| passport_clean_web | 10299 | 10399 | passportlbcpassportcleanweb | logbroker-client-passport-clean-web |
| passport_toloka | 10302 | 10402 | passportlbccleanwebtoloka | logbroker-client-passport-toloka |
| revoke_oauth_tokens | 10300 | 10400 | passportlbrevokeoauthtokens | logbroker-client-revoke-oauth-tokens |
| social_bindings | 10298 |10398 | passportlbcsocialbindings |  logbroker-client-social-bindings |
| takeout | 10294 | 10394 | passportlbctakeout | logbroker-client-takeout |
| xiva | 10295 | 10395 | passportlbcxiva | logbroker-client-xiva |
| ufo | 10296 | 10396 | passportlbcufo | logbroker-client-ufo |
| logbroker_test | 10304 | 10404 | passportlblogbrokertest | logbroker-client-logbroker-test |
| challenge_pushes | 10305 | 10405 | passportlbchallengepushes | logbroker-client-passport-challenge-pushes |
| mail_unsubscriptions | 10306 | 10406 | passportlbcmailunsubscriptions | logbroker-client-passport-mail-unsubscriptions |
| takeout-tasks | 10307 | 10407 | passportlbctakeouttasks | logbroker-client-takeout-tasks |
