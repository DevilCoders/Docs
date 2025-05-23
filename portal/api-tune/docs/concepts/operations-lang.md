# Смена языка пользователя

Настройка языка хранится в 39-м блоке куки [my](http://wiki.yandex-team.ru/MyCookie), она участвует в логике выбора языка контента, который будет предоставлен пользователю.

Для изменения языка необходимо обратиться к ресурсу:

```no-highlight
http://tune.yandex.ru/api/lang/v1.1/save.xml
```

{% note info %}

К ресурсу следует обращаться в текущем национальном домене `ua, kz, by` и пр.

{% endnote %}


**Параметры запроса:**
- `intl` — язык, который должен быть сохранен. Перечень возможных значений: `ru, uk, en, kk, be, tt, az, tr`. Если параметр не указан или имеет некорректное значение, то изменение языка не производится, а пользователь перенаправляется на морду;
- `retpath` — URL, на который пользователь должен быть направлен после выполнения запроса. Если параметр отсутствует, то пользователь перенаправляется на морду. Значение параметра должно быть [URL-кодировано](http://ru.wikipedia.org/wiki/URL#.D0.9A.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_URL) (urlencode);
- `sk` — секретный ключ ([SecretKey](http://wiki.yandex-team.ru/AlekseyPonomarev/secret-key)). Если этот параметр не указан, то операция смены языка выполнена не будет. При невалидном значении ключа пользователь будет перенаправлен на `yandex.(ru|ua|kz|...)/#sk` в зависимости от текущего домена. Например, `www.yandex.com.tr/#sk`.

Если пользователь обратился к доменам `ua`, `kz` и `by`, то запрос перенаправляется на `tune.yandex.ru`, для которого будет сохранено значение языка в куке. С помощью Паспорта будут обновлены куки для национальных доменов.

Если пользователь обращается к доменам `com.tr` или `com`, то перенаправления не происходит и кука модифицируется в том домене, к которому был сделан запрос.

**Пример запроса:**

```
http://tune.yandex.ru/api/lang/v1.1/save.xml?intl=uk&retpath=http%3A%2F%2Fwww.yandex.ru&sk=_15b7d7484b9fe720d9031598297f730e
```

#### Узнайте больше

- [liblang-detect](https://doc.yandex-team.ru/lib/lang-detect/concepts/about.html)