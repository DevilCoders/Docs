## Shard

Отвечает за процессинг оферов (полученных из [VOS](https://github.com/YandexClassifieds/vos2-autoru)), модификацию и упаковку индексов для отправки проиндексированных данных в S3 (откуда их дальше подберет [серчер](https://github.com/YandexClassifieds/auto/tree/master/auto-searcher) для ответа на поисковых запросов)


### Ручное добавление оферов
Мы можем вручную добавить офер (как если бы это делал VOS)

Редактируем `auto-shard/scripts/req.sh`, выставляем нужный OFFER_ID

```
cd auto-shard/scripts/ && ./req.sh
```

### Конвеер данных внутри шарда
Каждый офер, который проходит из ВОСа, проходит примерно такой путь в индексы (на примере офера Cars, для Moto\Trucks есть свои суффиксы):
```
OfferMessage (protobuf, приходит из ВОСа) 
-> Offer 
-> Unifier (обогащение) 
-> UnifiedCarInfo 
-> CarAdConverter (очищение для индексов) 
-> CarAd 
-> CarAdMessage (protobuf, кладем в поисковой индекс)
```

### Конвеер данных для trade-in
Генерация подписочного документа для оффера
```
ApiOfferModel.Offer (protobuf)  
-> CarAdMessage (protobuf) 
-> CarAd 
-> UnifiedCarInfo (+ processing by tradeInUnifiedProcessor)
-> CarAd 
-> Document (for subscription)
```
