# Заглушка для ошибок market-loyalty

### Описание

 Заглушка market-loyalty нужна для подмены возвращаемого результата на один из видов ошибок, для тестирования смежных компонентов.
 Ошибки в лоялти бывают двух типов: 
  1. купонные, например, COUPON_NOT_APPLICABLE - возвращается, как одна ошибка для всего запроса
  2. флэшовые или поайтемные, например, STOCK_OF_OFFER_EXCEEDED - возвращается, для каждого айтема своя
 Полный перечень ошибок [здесь](https://github.yandex-team.ru/market-java/market-loyalty/blob/master/market-loyalty-api/src/main/java/ru/yandex/market/loyalty/api/model/MarketLoyaltyErrorCode.java)
 Названия для дополнительных параметров ошибок [здесь](https://github.yandex-team.ru/market-java/market-loyalty/blob/master/market-loyalty-api/src/main/java/ru/yandex/market/loyalty/api/model/MarketLoyaltyErrorParam.java)
 
 Если используя заглушку, вы получаете 400, значит заглушка сработала, но формат файла error_config.json неправильный. 

### Шаги создания заглушки


1. Создаем акцию в тестовой админке [market-loyalty](https://admin.market-loyalty.tst.market.yandex-team.ru/promos). 
(Для этого может потребоваться выдача прав, за правами можно обратиться в pers-hotline или к @a-danilov.) 
Для флэш-акций не забываем указывать правильный shopId
2. Следует проверить, что сейчас траты купонов или флешей работают без ошибок. 
Подмена ошибок происходит только тогда, когда сам метод отрабатывает без ошибок. 
Иначе поведение заглушки не определено. Это связано с тем, что заглушка подменяет только ошибки, оставляя весь остальной результат прежним. 
3. Создаем данные для заглушки. Корень для расположения данных [тут](https://svn.yandex.ru/market/market/branches/test-util/market-loyalty/test-util/shops/).  
Создаем папку с названием совпадающим с uid тестировщика, внутри создаем папку с названием метода, который тестируем (calc или discount), теперь создаем файл с названием error_config.json
4. Идем в [swagger ручку с примером для генерации данных](http://market-loyalty.tst.vs.market.yandex.net:35815/swagger-ui.html#/stub-swagger-controller)
5. Если мы создаем ошибку для флешей, проверяем, что правильно задали feedId и offerId. В случае, если какие-то пары feedId и offerId не будут найдены, подмены результата для них не произойдет.
