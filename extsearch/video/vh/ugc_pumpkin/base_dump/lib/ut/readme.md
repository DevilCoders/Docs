Код в тесте проверят количество полей для похода в PG на проде и количество полей в тыкве.

Если вы добавили новое поле в запросе и тест упал, то нужно добавить это поле в:
1. [Запрос на YQL](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/video/vh/ugc_pumpkin/queries/create_video_item.yql).
2. [Процесс дампа из YT](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/video/vh/base_generation/lib/dumpers/ugc_index/video_item.cpp).
3. [Структура FlatBuffer](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/video/vh/ugc_pumpkin/base_dump/lib/flat/ugc_base.fbs64).

Почему deletedElementsFromPG равно 5 ?

Это количество полей, которые удалили из запроса в PG, но удалять из FlatBuffer поля нельзя, так как пострадает обратная совместимость.

Список удаленных полей:
- Resources
- ChannelResources
- InputWidth
- HasAudioStream
- InputHeight