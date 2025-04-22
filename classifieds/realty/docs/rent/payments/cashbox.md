## Пробитие чеков

Чеки в Аренде выбиваются при помощи отдельного микросервиса `realty-cashbox`.
- [Здесь](http://realty-cashbox-api-main.vrts-slb.test.vertis.yandex.net/swagger/) можно найти swagger тестового апи cashbox'a.
- [Здесь](https://yc.yandex-team.ru/folders/foo4nrk07dl14udeb4js/managed-mysql/cluster/mdbb38vf22c7s9ulq3i0?section=overview) можно найти тестовую базу cashbox'a.

### Функции сервиса

Бизнесово `realty-cashbox` выполняет следующие функции:
- выбивает автоматически чеки о платежах жильцов Яндекс.Аренды - за арендную плату и комиссию;
- выбивает те же чеки при создании их вручную из интерфейса [Cream'a](https://cream.test.vertis.yandex-team.ru/receipts);
- выбивает возвратные чеки для чеков, выбитых ранее;
- шлёт чеки в html-формате на почту жильцу.

### Принцип работы

С точки зрения взаимодействия с другими сервисами общая схема выглядит так.

![cashbox services](img/cashbox-services.png)

Жизненный цикл чека, выбиваемого автоматически, выглядит следующим образом.
- Вначале в Аренде жильцом успешно оплачивается платёж.
- В `rent-scheduler`'e через
[ручку поиска](http://realty-cashbox-api-main.vrts-slb.test.vertis.yandex.net/swagger/#!/receipt/searchReceiptRoute)
ищется, не был ли уже выбит чек нужного типа.
- Если чек не был выбит, процесс его пробития инициируется
[ручкой создания чека](http://realty-cashbox-api-main.vrts-slb.test.vertis.yandex.net/swagger/#!/receipt/postReceiptRoute).
- Далее в `realty-cashbox-scheduler`'е чек начинает обрабатываться `ReceiptWatcher`'ом.
- `SendReceiptStage` инициирует пробитие чека в White Spirit / Dark Spirit.
- `CheckReceiptStage` поллит статус чека в White Spirit / Dark Spirit, пока тот не будет пробит.
- `ReceiptNotifyStage` получает HTML чека от receipt renderer'a и отправляет его на почту жильца.
- `SendApprovedReceiptStage` отправляет в кафку сообщение о том, что чек был успешно пробит.
- Далее `rent-consumer` вычитывает это сообщение из кафки и сохраняет в платёж краткую информацию о пробитом чеке.
- После этого чек можно найти на [странице с чеками](https://arenda.test.vertis.yandex.ru/management/manager/flat/f2c7e22e3d614e57883de779fd3698d1/payments/8bd4dd010ef6a7742cf520a521a25735/receipts/) по данному платежу в админке Аренды.
- При необходимости из неё можно перейти по ссылке в Cream и сделать возврат чека.
