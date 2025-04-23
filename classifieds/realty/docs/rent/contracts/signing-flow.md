## Электронное подписание договора аренды

Электронное подписание договора аренды (далее _ДА_) призвано автоматизировать и сократить количество действий, которое необходимо совершить для заключения сделки, таких как:

- Ручное формирование ДА координатором
- Отправка ДА на ознакомление собственнику/жильцу и последующее внесение правок
- Отправка распечатанного ДА обратно координатору

Новый процесс лишен этих недостатков.

### Последовательность подписания

![https://mermaid-js.github.io/mermaid-live-editor/edit#pako:eNp9Uk9PwjAU_ypNTyOBi_HEwQTFm4lGTDwwDg0rsMgGGZ2GAIlAogcOejDeNPEbDAKyiMBXeP1Gvq4bBiQ22fr6-n5_-toOLTcsTrO06rFmjZxdmi7BceJxJrgBH7CCOUwhgCWEMCPwAs8pkskc5T1WEbo2Co1iNJWizS68ywGs5T3iJvAFAZF9JBrLYbdgV13brWpkzmlcsdbNHpk5hriUjxASmKjCXdWYyCjGQaKsqMYE1jhN8R_KvhyhiQBmchCpc-u4fX7nco9sEWn0mxzCJyzliKCPOXzDDB2pL5RP3diuhv2CN4Tay2aZOHpFqgXKP_zvKmZUA2HXzBbo6oK1He6K4sEhwV4E2MaAoBv8rZBmgZmBHJbinicZtY1KqIGbSk2lu7mysG-5Ftlm3wNfqkv4y7HTf24lR8azxlcaqRhFPZdSNE0d7jnMtvCNdVSNSUWNO9ykWQwtXmF-XZjUdHtY6jctfHanli0aHs1WWL3F05T5olFou2WaFZ7Pk6K8zfDJOjrZ-wH9xUxn](../img/contract-signing.png)

### Создание договора
Происходит в ручке [создания договора](./upsert.html#create).

### Отправка собственнику на ознакомление {#send-to-owner}
Происходит в [ручке смены статуса договора](./change-status.html#send_to_owner).

- Статус договора меняется на `Signing`
- Происходит генерация документа ДА в Dochub и приобщение его в `RentContract.addContractDocument`
- Из анкеты в договор записываются следующие поля
  - Арендная плата
  - Сумма страховки (вычисляется на основе АП)
  - Размер комиссии
  - Тип недвижимости
  - Можно с животными
- У собственника
  - Приходит пуш "Подпиши договор"
  - В [ручке получения квартиры](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/getFlat) появляется нотификация "Подпиши договор"

### Просмотр перед подписанием {#summary}
[Ручка краткой информации о договоре](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/getContractSummary) возвращает:
- Краткую информацию о договоре (см. `ContractSummaryBuilder`)
- FAQ (разные для собственника и жильца), доступные для [редактирования в Пальме](https://palma.test.vertis.yandex-team.ru/dictionaries/realty/rent/contract/faq).
- Собственнику: вопрос/ответ собственника с координатором (если есть)
- Жильцу: последняя версия правил пользования сервисом

### Запрос изменений в договоре собственником {#request-changes}
Происходит в [ручке](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/requestContractChanges).

- Только для собственника и ДА в статусе `Signing`
- Дернуть ручку можно только один раз
- Создает новую задачу в АМО с комментарием собственника
- Записывает комментарий в `ContractData.owner_comment`
- Сбрасывает договор в черновик
- У собственника в [ручке получения квартиры](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/getFlat) появляется нотификация "Договор отправлен менеджеру"

### Подписание договора
Может быть произведено:
  - Собственником/жильцом
  - Вручную координатором в ручке [смены статуса](./change-status.html) договора

Для подписания собственником/жильцом необходимо [запросить код в смс](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/askContractSignCode):

- Собственник может запросить код только для договора в статусе `Signing`
- Жилец может запросить код только для договора в статусе `SignedByOwner`

А потом отправить его в ручку [подписания договора](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/signContract).
- Которая вернет идентификатор первого платежа для жильца (**но может его не возвращать**, потому что его создание происходит асинхронно в `CreatePaymentStage`, это нужно учитывать)
- Даты подписания каждой стороны записывается в `ContractData.signs`, чтобы потом фигурировать в pdf-версии договора

#### Подписание собственником {#sign-by-owner}
- Статус договора меняется на `SignedByOwner`
- Из Dochub выбирается договор созданный на предыдущем этапе, обогащается информацией о дате подписания собственником и приобщается к ДА
- В стейдже `CreatePaymentStage` начинают генерироваться платежи для оплаты жильцом
- У собственника в [ручке получения квартиры](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/getFlat) появляется нотификация "Вы подписали договор"
- У жильца
  - Приходит пуш "Подпиши договор"
  - В [ручке получения квартиры](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/getFlat) появляется нотификация "Подпиши договор"

#### Подписание жильцом {#sign-by-tenant}
Жилец должен отправить версию правил пользования сервисом, полученную из [ручки краткой информации о договоре](#summary), в противном случае будет `INVALID_TERMS_VERSION`. Если все хорошо:
- Статус договора сменяется на `Signed`
- Из Dochub выбирается договор созданный на предыдущем этапе, обогащается информацией о дате подписания жильцом и приобщается к ДА
- У жильца
  - В [ручке выбора квартиры](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/getFlat) появляется нотификация о необходимости оплатить первый месяц
  - В случае неоплаты в течение 1 часа приходит пуш с напоминанием об оплате

### Активация договора {#activate}
Может быть произведена:
- В `ActivateOrDraftStage` при оплате жильцом первого месяца аренды
- Вручную в [ручке смены статуса ДА](./change-status.html#activate)

При этом:
- Статус жильца сменятся c `TenantCandidate` на `Tenant`
- Статус квартиры изменяется на `Rented`
- Статус договора изменяется на `Active`
- В [ручке выбора квартиры](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent/getFlat)
  - Собственник получает нотификацию "Договор подписан"
  - Жилец получает нотификацию "Вы подписали договор"

### Сброс договора в черновик {#draft}
Может быть произведен:
- Собственником в [ручке комментирования договора](#request-changes) при запросе изменений
- В `ActivateOrDraftStage` при неоплате в течение 24 часов после подписания ДА жильцом
- Вручную в [ручке смены статуса](./change-status.html#draft)

При этом:
- Удаляются сгенерированные документы из Dochub
- Очищаются поля, заполненные во время отправки договора собственнику (см. `RentContract.draft`)

### Генерация и скачивание pdf-версии
Документы [хранятся в Dochub](https://palma.test.vertis.yandex-team.ru/dictionaries/realty/dochub/documents). Генерация происходит:
- В [ручке скачивания файлов](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/files/getDownloadUrl)
- При отправке собственнику на ознакомление
- При подписании собственником/жильцом (обогащается предыдущая созданная версия)

При этом:
- При генерации всегда используется версия шаблона, указанная в договоре [на этапе его создания](./upsert.html#create)
- Для договора в статусе `Draft` всегда запрашиваются данные для его формирования (квартира, анкета, собственник, жилец и сожители) из MySQL/Palma и отправляются в ручку `DocumentService.CreateDocument`, предварительно сформировав хэш от отправляемого шаблона, чтобы идентификатор документа получился что-то типа `rent.contract.{contractId}.{templateHash}`
- Для договоров в статусе `Signing`, `SignedByOwner` и `Signed` скачивается уже созданный договор
- Для договоров в других статусах мы забираем из Dochub договор, сохраненный в `ContractData.contract_documents` в статусе `Signed`
