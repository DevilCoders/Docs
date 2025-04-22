# Работа с картинками в Недвижимости

## 1. Общая картина
(респект Никите Грищенко за инфу)

### 1.1 Mobile apps
Ручка [photo.json](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/1.x/#!/photo/photoRoute) в realty-gateway
Принимает сконвертированный файл, прокачивает его через аватарницу и возвращает ссылку на оригинальный файл + все размеры

```
{
  "response": {
    "path": "https://avatars.mdst.yandex.net/get-realty/3019/add.a64d4aca3e7a32c34f4634e6c26b6db7.realty-api-vos/orig",
    "sizes": [
      {
        "variant": "1200x630",
        "path": "//avatars.mdst.yandex.net/get-realty/3019/add.a64d4aca3e7a32c34f4634e6c26b6db7.realty-api-vos/1200x630",
        "height": 630,
        "width": 1200
      },
      {
        "variant": "alike",
        "path": "//avatars.mdst.yandex.net/get-realty/3019/add.a64d4aca3e7a32c34f4634e6c26b6db7.realty-api-vos/alike",
        "height": 60,
        "width": 80
      },
      ...
    ]
  }
}
```
### 1.2 Web app (фронт)
Веб-приложение само загружает картинку в аватарницу, нам присылает только ссылки при создании оффера (или черновика).

### 1.3 Feeds
В случае фидовых офферов мы прокачиваем фотографии в ru.yandex.vos2.watching.stages.mds.ExternalImageUploadStage. 

Пример с фидовой фоткой externalUrl foo.com/iamge1.jpg offerId:10050
1 EIUStage pica {"key" -> "offer.100500", url -> "foo.com/iamge1.jpg",partitionId -> "100500", hashid -> "ae1343dfdfd"} -> 

### 1.4 MdsMetaStage (для всех платформ)
См. ru.yandex.vos2.watching.stages.MdsMetaStage.
Еще раз ходим в picaPica, дожидаемся завершения обработки meta. Парсим и складываем в двух форматах старый и unified(новый),в raw версии меты  есть все новые поля которые для нас делает копьютерное зрение, но мы парсим так же только опредленное подмножество, которое нас интересует.

### 1.5 Preview
В самом оффере мы храним preview фоточек (в низком разрешении, кодируем в виде строки), которые можно использовать для быстрого показа (или в случае проблем с доступом к аватарнице).

### 1.6 Известные проблемы
* Здесь бывают проблемы с ограничениями cdn создателей фида, и при больших фотках/большом кол-ве начинает отваливаться. Нужно научиться делать похостовые ratelimiter'ы
* Есть проблема с использованием дублей фоток в разных офферах 
* Новая pica не позволяет прокачивать мету для картинок загруженных напрямую в аватарницу


## 2. Подробнее про фидовые офферы
(респект Илье Кузнецову за инфу)

Фидовые офферы поступают из feed-processor'а в vos-consumer (через кафку) в виде FeedOfferEvent, См. ru.yandex.vos2.realty.processing.updates.FeedOfferProcessor и ru.yandex.vos2.realty.processing.updates.OfferUpdatesService#upsert

В OfferUpdatesService#merge происходит merge картинок из эвента и из текущего оффера в базе воса. Там есть предохранитель, чтобы при частых изменениях урлов картинок в фиде (таймстемпы!) мы переставали обновлять урлы на какое-то время (см. фича-флаг PhotosUploadOverLimit, его generation - количество дней, спустя которое урлы снова начинают обновляться). Часть фоток в оффере залочены (hasLock), они не обновляются (про локи см. далее).

В результате мержа часть фоток помечается как удалённые - см. вызов ImageUtils#mergePhotos, в нём setDeleted

Непосредственно удаление фоток происходит в vos-scheduler, см. ru.yandex.vos2.watching.stages.RemoveOldImagesStage и ru.yandex.vos2.watching.mailbox.RemoveOldImagesProcessor.  Для этого нужно сходить в picapica и в mds, см. ru.yandex.vos2.realty.util.PhotoRemover:
1. В picapica нужно удалить фотку из её кеша, это делается вызовом в синхронную ручку - ru.yandex.realty.clients.picapica.PicaPicaClientImpl#clearCache
2. В mds нужно удалить саму фотку, и там это делается асинхронно вызовом в ручку - ru.yandex.vos2.services.mds.MdsClient#delete. От ответа этой ручки зависит то, как пометится фотка в оффера воса, может быть несколько ситуаций:
   * При первом вызове ручка mds вернёт Accepted, и тогда для фотки в оффере сохранится lock - PhotoRemover#lockPhoto, и оффер порескедулится. Это будет означать, что мы начали удалять фотку, и поэтому об этом нельзя забывать в vos-consumer.
   * При втором вызове ручка mds вернёт Ok (т. е. фотка была успешно асинхронно удалена), и тогда для фотки снимается lock - PhotoRemover#unlockPhoto, и она удаляется из оффера полностью - RemoveOldImagesProcessor#updateOffer

## 3. Схематично
![Realty photos - feeds](img/Realty_Photos_Feeds.png)

------------------------------------------------------------------

![Realty photos - web](img/Realty_Photos_Web.png)

------------------------------------------------------------------

![Realty photos - mobile](img/Realty_Photos_Mobile.png)