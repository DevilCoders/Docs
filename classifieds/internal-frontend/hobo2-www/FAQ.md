# Типичные кейсы

## Как добавить таску Хобо2 очередь?
1. Идешь в прод Хобо1, берешь таску из нужной очереди в проде. Сразу нажми "Сделать новой", потому что это прод вообще-то.
2. Смотри в нетворке json этой таски, там будет payload вида:
```json
{
  "payload": {
    "type": "external",
    "ids": [
      "CARS:auto_ru_36201940"
    ]
  }
}
```
Копируй его!
3. Иди в Swagger в ручку http://hobo-api.vrts-slb.test.vertis.yandex.net/swagger/#!/queue/createSingleTask
4. Слева в инпут **body** добавляй свой payload
5. Укажи **X-Yandex-User**, например `staff:my-staff-id` или staff-id твоего руководителя
6. Выбери **queue** в селекте, которая тебе нужна.
7. Жамкай "Try it out".
8. Profit.