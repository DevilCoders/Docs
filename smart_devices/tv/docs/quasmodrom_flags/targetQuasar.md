# targetQuasar
**Type:** String
**Default:** prod

**Related tickets**
[TVANDROID-4919](https://st.yandex-team.ru/TVANDROID-4919)

**Context**
```json
{
  "targetQuasar": "prod / testing / localhost"
}
```

**Description**
`!!ИСПОЛЬЗОВАТЬ ОСТОРОЖНО!!`
Флаг выставляет значение url quasar и billing бэкендов
prod - [https://quasar.yandex.net](https://quasar.yandex.net)

testing - [https://quasar.yandex.net](https://quasar.yandex.net)
/dev
localhost - http://localhost:8888 (для автотестов, чтобы мокать получение подарка)

Иметь ввиду: ваш девайс должен быть прописан и в тестовой и в продовой админках (например, для модуля, тут [https://quasmodrom-test.quasar-int.yandex-team.ru/quasarbackend/device](https://quasmodrom-test.quasar-int.yandex-team.ru/quasarbackend/device)
 и тут [https://quasmodrom.quasar.yandex-team.ru/quasarbackend/device/)](https://quasmodrom.quasar.yandex-team.ru/quasarbackend/device/))
 и в обоих должен быть конфиг.
При получении флага рекомендуется проверить и продовый и тестовый конфиг (чтобы не было ситуациации постоянного переключения).
Работает только на не-юзер билдах.
После применения флага рекомендуется перезагрузка.


