# Подписки на сервисы

В разделе описан вспомогательный метод для просмотра подписок (subscription).

{% note warning %}

Описываемый метод служит для тестирования и отладки. В промышленной эксплуатации Паспорта данный метод не используется, а параметры подписок возвращаются по запросам к Черному ящику.

{% endnote %}


## Синтаксис запроса {#id2018DE01}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<subscr>
  & uid=<id>
```
### Параметры
#### mode
*Обязательный параметр*
#### target
*Обязательный параметр*
#### uid
*Обязательный параметр*

Идентификатор пользователя, для которого нужно получить подписки.

> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=subscr&uid=1130000000000740`
> Запрос выводит данные о подписках аккаунта 1130000000000740.

## Формат ответа {#id006C2EC3}

Ответом является XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors> </errors>
  <operation>list</operation>
  <subscriptions>
    <login>petrov.petr@okna.ru</login>
    <loginrule>1</loginrule>
    <sid>8</sid>
    <suid>1130000000001758</suid>
  </subscriptions>
  <subscriptions>
    <login>petrov.petr@okna.ru</login>
    <loginrule>1</loginrule>
    <sid>100</sid>
    <suid>1130000000001760</suid>
  </subscriptions>
  <subscriptions>
    <login>petrov.petr@okna.ru</login>
    <loginrule>1</loginrule>
    <sid>2</sid>
    <suid>1130000000001759</suid>
  </subscriptions>
  <target>subscr</target>
  <uid>1130000000000741</uid>
</mdapi>
```

Информация о подписках содержится в элементах `subscriptions`, а ее интерпретация выполняется сервисами.

## Сообщения об ошибках

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`. Ниже показан пример сообщения об ошибке.

#### errors	
Содержит элементы `error`, если при выполнении запроса возникли ошибки. Если ошибок не было, в ответе выводится пустой элемент errors.

#### error	
Сообщение об ошибке. Ниже перечислены возможные сообщения:

* `not-found` — указан несуществующий идентификатор пользователя (`uid`);
* `int-error` — ошибка на стороне Паспорта, причина ошибки не уточняется.