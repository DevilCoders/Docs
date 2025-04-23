# Расследование проблем с картинками

## Где у оффера хранятся картинки?
### В [ecom/export выгрызке](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/ecom/export/offers/merged "Экспортная выгрузка")
[Формат экспортного оффера](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/external/Offer.proto)
- [Картинки, пришедшие от партнера](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/external/Offer.proto?rev=r9384916#L83). Хранятся url, ведущие на картинки на сайте партнера.
Эти картинки должны скачаться пикроботом и положиться в аватарницу в конкретный namespace
- [Картинки, загруженные в аватарницу](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/external/Offer.proto?rev=r9384916#L87).

## Диспатчер

Иногда полезно грепать логи [диспатчера](https://deploy.yandex-team.ru/projects/market-datacamp).
Там к примеру можно найти информацию о некорректности URL.
[Пример](https://paste.yandex-team.ru/9235419 "Пример ошибок о некорректности URL в логах диспатчера")  

## Стейт пикробота

Пикробот сохраняет [стейт](https://yt.yandex-team.ru/arnold/navigation?offsetMode=key&path=//home/market/production/indexer/picrobot/state/state)

Стейт пикробота хранится в сжатом виде.
- Получить разжатый стейт для конкретной картинки по URL. 
Ручка пикробота - `http://datacamp-picrobot.pre.vs.market.yandex.net/state?url=<URL>`
[Пример стейта по URL](http://datacamp-picrobot.pre.vs.market.yandex.net/state?url=https://i4.stat01.com/2/963/109624312/afacdb/polok-termoabash.jpg "Пример")
- Получить разжатый стейт для набора картинок в YT табличку. 
Тулза - [picrobot_state_decoder](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/picrobot_state_decoder "тулза для декодирования набора стейтов пикробота")

ps: Картинки лавки и еды до пикробота не доходят, так как они уже загружены в нужный неймспейс

## Логи самовара
Логи смотреть тут - `https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer`
[Пример логов самовара по URL](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer?key=https%3A%2F%2Fi4.stat01.com%2F2%2F963%2F109624312%2Fafacdb%2Fpolok-termoabash.jpg&keyType=url "Логи самовара для URL")
[График реджектов самовара](https://solomon.yandex-team.ru/?project=samovar&cluster=primary-arnold&service=samovar_combustor_url&l.path=%2FCrawlCounters%2FPolicy%2FRejectedBy*&l.ZoneName=Total&l.host=cluster&l.Component=Crawl&l.PolicyName=data-camp-images&graph=auto&checks=-Total&b=31d&e=)
В нем:
- `RejectedByGlobalBorder` - не удалось скачать из-за превышенного `лимита по квоте`
- `RejectedByHostBorder` - не удалось скачать из-за превышенного `хостового лимита`
- `RejectedByIpBorde` - не удалось скачать из-за превышенного `айпишного лимита`

## Логи зоры
https://wiki.yandex-team.ru/robot/zora/developerguide/logi-zory/

## Примеры дебаг запросов
- [Оффера директа без аватарок, но с первой оригинальной картинкой](https://yql.yandex-team.ru/Operations/YnU2LLq3k0t8E0UoyzdUEDSYqids6GkQWUq05IqKH5o=)
- [Процент оффером директа без аватарок по бизнесам](https://yql.yandex-team.ru/Operations/YnVA99JwbH5UGiX6oQ35bP9Jnq04CvVfOugvN1C3RJE=)
- [Количество офферов по цветам без аватарки, но с первой оригинальной картинкой](https://yql.yandex-team.ru/Operations/Ynuqkbq3k0t8IDLsZPFweYZmMdtOawikFUS_Um4gmAw=)
- [Оффера (директ, дикие) без информации/с информацией в стейте пикробота](https://yql.yandex-team.ru/Operations/Yn5xm1Z1O6FkFNz_fZa1il6516uuYQjyx2mTOLnC9m4=)


[Пример дебага проблем с директом](https://wiki.yandex-team.ru/users/fadeevsergey/problemy-s-kartinkami-direkta/)
