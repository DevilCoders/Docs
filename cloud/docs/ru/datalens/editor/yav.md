
# Секретница (YAV)

ChartEditor позволяет работать с секретами из [Секретницы](https://yav.yandex-team.ru/).

## Как привязать секрет к чарту {#how-to-link-secret}

- в панели управления нажать на иконку ![связка ключей](../../_assets/datalens/internal/editor/secret-keys.png)
- в диалоге "Секреты" нажать на кнопку "Добавить секрет"
- появится список секретов, доступных в [Секретнице](https://yav.yandex-team.ru/)
- выбрать секрет
- добавить ключ секрета и название для алиаса

[В коде](#access-to-secrets) секреты будут доступны через алиасы, поэтому важно, чтобы алиас имел уникальное название.

Все добавленные секреты будут забираться из самой последней версии секрета в [Секретнице](https://yav.yandex-team.ru/).

## Права доступа на чарт с секретами и безопасность {#permissions}

В целях безопасности выполнять скрипты в ChartEditor можно начиная с прав на "Редактирование" и выше.
Это правило не распространяется на чарт внутри дашборда или в других местах, так как там выполняется опубликованный чарт.

Если вы выдаете пользователю права на "Редактирование" и выше, то фактически даете ему доступ на просмотр ваших секретов.

При выводе информации о секрете в `console.log` будет выводиться случайно сгенерированная строка вида `sec-fe523b7330-ret`. Это сделано для того, чтобы секрет случайно не попал в логи чарта.

## Доступ к секретам из кода {#access-to-secrets}

Для получения секретов в коде нужно использовать метод `ChartEditor.getSecrets()`. Он вернет объект с секретами, где ключи объекта - это добавленные алиасы, а значения - непосредственные значения секретов.

Для примера представим, что добавили секрет с алиасом `clickhouse`.

```js
const secrets = ChartEditor.getSecrets();
const clickhouseSecret = secrets['clickhouse'];
```


