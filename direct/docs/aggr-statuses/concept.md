[Код агр. статусов](howto-code.md)<br />
[Диагностика статуса объекта](howto-diagnose-status.md)<br />
[Эксплуатация системы статусов](jeri.md)<br />


# Агрегированные статусы

Сквозная система статусов для кампаний, групп, объявлений и фраз.

Для истории, оригинальный фичадизайн: [wiki://direct/development/design-review/201909-aggregated-statuses](https://wiki.yandex-team.ru/direct/development/design-review/201909-aggregated-statuses/)

Пользователю важно видеть фактический статус объекта — идут ли показы или нет.

Для этого на объектах верхнего уровня (группах, кампаниях), нужно учитывать состояние подобъектов — ключевых фраз, объявлений.
Учесть состояние всех групп кампании на странице самой кампании — можно, но если мы отображаем грид кампаний, где таких кампаний может быть тысяча, то подгрузить из БД все подобъекты и посчитать по ним статусы будет слишком долго с точки зрения отзывчивости интерфейса.

Поэтому приняли решения вычислять статусы заранее, при каждом влияющем на статус изменении объекта и сохранять результат вычисления в MySQL. При этом мы агрегируем статусы снизу вверх, так статусы объявлений влияют на тот статус группы, который мы на группу сохраним в БД. Также статус групп будет влиять на сохраненный статус кампании. Т.е. мы **агрегируем** статусы снизу вверх. Такой, сохраненный в БД, статус мы будем называть **собственным статусом** (`SelfStatus`) объекта.

При этом показывается или нет объявление зависит например от того, есть ли деньги на кампании, и именно этот честный статус мы хотим отображать пользователю в интерфейсе. Поэтому в момент показа объектов нижнего уровня мы получаем из БД статусы вышестоящих объектов и учитываем их в отображаемом статусе. Также в момент отображения учитываются такие факторы как временной таргетинг и время старта/окончания кампании. Такой, отображаемый пользователю, статус мы называем **эффективным статусом** (`EffectiveStatus`).


## Путь данных при вычислении статусов

Тригером для пересчета статусов служит binlog, обрабатываемый в ESS, на основании такого тригера работает job-а `AggregatedStatusesProcessor`, которая достает по id-шникам объекты из БД, пересчитывает их статусы и сохраняет в базу.

При открытии объектного грида вместе с объектами из БД выгружаются их статусы и статусы вышестоящий объектов, они накладываются друг на друга по определенным правилам и отображаются на фронт.

Таким образом путь данных можно изобразить примерно так:
```
binlogbroker -> ess rules -> ess logic processors -> core (jobs) -> MySQL ----> direct-web -> front grid view
                                                                      \-> YT -> direct-web -> front filtration
```

## Этапы вычисления статуса
Вычисление статуса можно разделить на следующие этапы:
1. На основании полей объекта (fields) вычисляются "состояния" объекта (States), коих может быть несколько, так кампания может быть одновременно завершенной и на ней может не быть денег;
2. Для объектов нижнего уровня — объявлений и условий показа, по стейтам вычисляется собственный статус (SelfStatus) и сохраняется в базу;
3. Счетчики (counter) по стейтам и собственным статусам объектов сохраняются в виде json-структуры на объекте верхнего уровня.
4. Для объектов имеющих подобъекты (кампаний и групп) собственный статус вычисляется с учетом стейтов объекта, а также с учетом счетчиков по стейтам и статусам его подообъектов;
5. В момент показа из БД выгружается статус объекта, статусы его родительских объектов, на основании чего отображается эффективный статус.

Условно подсчет статусов можно отобразить [диаграммой](https://drawio.yandex-team.ru/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1#R7V3ZcqM4FP0aP3YKJITEY5ytp7qnpmtS1cvTFDayzTQBDyadpL9%2BxGajBYwxKDhxHhIQQsC9525Hgkzg1cPzXeyuV39GHg0mwPCeJ%2FB6AoAJTcL%2BpC0veYuNrbxhGfte0WnXcO%2F%2FpkWjUbQ%2B%2Bh7dcB2TKAoSf803zqMwpPOEa3PjOHriuy2igL%2Fq2l1SqeF%2B7gZy6zffS1Z5K0HGrv0j9Zer8sqmURyZufOfyzh6DIvrTQBcZD%2F54Qe3HKvov1m5XvRUaYI3E3gVR1GSbz08X9EglW0ptvy825qj2%2FuOaZi0OcEpbiN5KR%2BdekwSxW4UJ6toGYVucLNrnWaPR9MBDLa3Sh4CtmmyTfrsJ9%2FT5gtU7P0oj4RJ%2FFI5lO7%2BKAb4lybJSwEB9zGJWNPuup%2BjaF2MIT9aiQw3XtKiqYBZ%2BhCVPsWz39HogbIrsw4xDdzE%2F8Wr2y1Qs9z22576JfLZVYFRItwB%2BSkFviGC%2FBCb6DGe0%2BKsnfzZRuU2dk2ZVmpUag6iooqCKjrZHtoqKDvWVkWbJI5%2Bbi0GspaFHwRXURDF2Z1DD1HiWduelSMEzKBtsyPL2PV8dv3KMQd7BsZNEMjFzUGgiorSHQ0OC8jDAmGHHyK%2FqT5gUTzlLzd4LO72PnET5jNFsPBQeFr5Cb1fu5mwnpjz5uFRK%2BBfNE7oc6PsamQAsZ3vP%2B0cqVm6v1XFidpGvbg5QTVIBUtSuVksWIBIVQqMVEKPTEJ2wC45ncVsa5lsn3pEMrOho09mJpSEduU%2BrF1%2FGVZFVZGP%2Fd9jGp%2BmiyhMPmwyt3DJOgC4fs7kUR6vlS8TS8ILkfcHYRRSwXkUTW6Q3ha8njNhU9Y%2BTYXss8B9WRx48D0vc4EqrfF6TW%2B%2FcGoA9qRIzCsSIFNSpKXQI%2BhDj0jSY5%2BRo20MEKVanxQIsWFB5nQ%2BV8UG%2B4rcTG%2FVsYG69iyLG3LsaRUtTEW46D2JaK1C2auXJpiKtY0RmoAZoWSBtz4NvK3nY7eRD1djniwpXaeb85fAZ2CI9%2FvAWY6az7OgBgUDOElANAYW025hXKF3mdYeqeQCd7Px57yQJMtoSIrrrWYUOZaJj0iyKvpCCnWVbT2n6Ai0S9H3D2QNltSZcv5S2uxm7Ybd7f9yuWTHrpiVsqipzIC2niG%2F0El7BsuWo%2B5wnoEMpLN7GizYNkvF2E4426R%2F6jPYt6Q%2FZOn07M5YPHvrfGhGkIWMgfIhInt2PC7HbiAOLdi2Ozp2JAxkCgP159jBMCTO6%2FFsZTAdmlGxgM3paECird9y6XCiDZ4a0VZioIoLaOjBBbR5XCCMBrNdmR8ZCdUmCkEr1aZgIE%2BCaxOFppVrAzJHc%2BndMRGsO1Bt75hnswxeiTp5NtCGCjjzbGKwUDAG%2FScRrXVYX2ifiTbRQ2ol2oCqnH6%2FRFs5Qd8px9JTj4kpemeiTRpoOKINqIr%2BM9F2qGfQSrRhhSPouz7Dx9VggsRFf%2BFSslAH3jmhs4XaX2AWeem2VPw%2BqRT6u3vOdq%2BfJ5Wi8vql2GvlZ0qfwhH6bXmfIx0IcAzBgQhoqbF7FgPcl0q3ddphU38daDj8dQhp9EdSfwMKeM3voKsTKmV%2BZo57c0hamWNoKvT3KqnKKJhjlQtpPZWuJ1WBkLfoztQxJMJAw1HHUAGqk6aOoaY1mrZtcToyLdBK2V10BE9HR6Moa0oMcKtuTE24MHhcQJsMZrujXaUpCsG0kcbAKbOgJ0EdS8gpC1QtQpNpx6kbhjQ%2BM8cH6dDidViyxBqIY6giHfsLG2%2BUOIaKBQn9pxCtdVi%2F2udMHIv%2BEWuMKWX80jZ7L7AwkJCxc0c1%2FFC294XGPpN5iqT2pJGlyO5LZrXnLO5QrgfVLBauK%2BjE%2FhaxBPQdx%2FVYKq6gP66nIWc6ZXpHdCgAaaR3ynLxTO%2FUGnuZyI%2BE3kEY80aMO9I7NhAGAoPRO2iYuPV69A7SNGsg0juI2Beolbq7aMk%2BHS2NguBBiuUeNtCEDCFqEBOIyOjRfuWibqQUj204FxoTciRXSidJ8mAHahWbvDJh6nubM8lzFMlDLIUOh%2BJ5bNW87pnn2RMxbC25RGsd1tdrZ55HdJHI1BpZ7GGSMY7q4Yo1geohzpGvapwg1VPmbmOkegC%2FfAgXb%2FTVUj1Cf1R8OKF2WSKxm%2FofTQ2Voj1TQ0elaYah1QfJLwXJTun9kEMq94DG9T0AkRxygNGSL9hLDxEsDdVfgWm3mTXcg7T9Majp618l9swJFCZD%2BsVeK6SpXiMZ1yIz0wAC0Dq%2Fn8wPREQ6sz%2BQkTt3%2Bo9jzDD59O2r9%2FHrfPnp5kP5zcYh8yzQOKc25jSLPcIuy0p3uCSrcS22ANROL9rmi7N75862r5CWyY5DuoF3GxK2i6dNveDVPh98YQjwNcEh5fqo6oRmcKsriENRrVoDmJcUr11BmE5zRSD2t2wiQLhSEeylp7ev1x38vpRQmFjDfW1SbWIa6vCm8PDG6vB6o%2BtmX6iXCHH4wgveNsrX6%2BsXXgjVeJE91YMeN%2FXfa3vCJ18M1LUIkG%2FEvEDY2f0MZYvlcuV%2BzY5P7kHTh0qO%2FCJws9XpqCFUnwhuvZRhYPMRPiBqI6sRhWJ%2FiJ1JrTl0ABse5M0GHmz43YGtNTWiGWzkMLAR0O8iOWxoAFtDQgHGDDbP3ayyx2yc5973adtXm1BTZ5DKz3Bw761%2BYIf%2FWiwCP0xXDUyYkqdgwmRAptlvnLWQbNvMtqfZb5T9vq4cvd2dDoyb%2B3sJavJsePtZ7phu%2FN%2FuLBsqVWRheWxcNJ2g63QsBqWcsK8oUKK7FTqtZcBNad4DqxhwPNAst1qhyuXxkkL%2FfgwTlvv2qNBvdJa6ny9%2FvAG18k4WQ6JQKzC0qtXp0zGPayHb%2FrKqd5JNslzIYk87ekzBNu8fq791kEp0kF4%2FbqkBHU3LWEaAjhYabYsO8vrgAIqIIKLl6OmrIfL6LqrXM8MkahW1U%2Bl%2BP4TMtkjbDw%2B2u%2Fs3Vnn33f8Kgzf%2FAw%3D%3D)

## Таблицы для хранения статусов
* [aggr_statuses_campaigns.schema.sql](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema/ppc/aggr_statuses_campaigns.schema.sql)
* [aggr_statuses_adgroups.schema.sql](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema/ppc/aggr_statuses_adgroups.schema.sql)
* [aggr_statuses_banners.schema.sql](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema/ppc/aggr_statuses_banners.schema.sql)
* [aggr_statuses_keywords.schema.sql](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema/ppc/aggr_statuses_keywords.schema.sql)
* [aggr_statuses_retargetings.schema.sql](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema/ppc/aggr_statuses_retargetings.schema.sql)


## Какие бывают статусы
Каждый статус это иконка с цветом.
Всего есть 13 статусов:
```java
    RUN_OK, RUN_PROCESSING, RUN_WARN,
    PAUSE_OK, PAUSE_WARN, PAUSE_CRIT,
    ON_MODERATION,
    STOP_OK, STOP_PROCESSING, STOP_WARN, STOP_CRIT,
    DRAFT, ARCHIVED;
```
где RUN — идут показы; PAUSED — показы приостановлены; STOP — показы не идут; и т.д.

OK, WARN, CRIT — зеленый, желтый и красный соответственно цвета иконок. Зеленый — все хорошо и как ожидается; желтый — есть что улучшить; красный — требуется внимание клиента, что-то идет не так.
 	 
PROCESSING - для смартов и ДО, пока у них идет генерация в BL (из-за чего показы либо не идут, либо идут - но показывается старая версия). Отображается как часики. История: [DIRECT-132731](https://st.yandex-team.ru/DIRECT-132731)

DRAFT, ARCHIVED и ON_MODERATION — отображаются серым цветом.

При вычислении статуса мы также сохраняем в БД список "причин" (reasons), которые привели к таком статусу, Например `STOP_CRIT + CAMPAIGN_ADD_MONEY_TO_WALLET` — кампания остановлена (иконка красная) по причине нехватки средств.


## Пример (структура) хранения статуса в БД

JSON в поле `aggr_data` соответствующей таблицы, пример для кампании:
```json
{
    "s": "ARCHIVED", /* статус */
    /* "r": [ список причин ] - для статуса ARCHIVED пустой */
    "sts": [ /* states - стейты объекта */
        "ARCHIVED",
        "DOMAIN_MONITORED"
    ],
    "cnts": { /* counts - счетчики подобъектов */
        "s": { /* по статутса */
            "RUN_OK": 9,
            "ARCHIVED": 5,
            "STOP_CRIT": 1
        },
        "sts": { /* по стейтам */
            "HAS_NO_EFFECTIVE_GEO": 1
        },
        "grps": 15 /* всего групп в кампании */
    }
}
```
