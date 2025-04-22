# Метод mdDomains

Возвращает список доменов в текстовом формате.

{% note warning %}

Данный метод служит целям отладки на тестовых серверах. Использовать его на промышленных серверах категорически не рекомендуется, поскольку он сильно нагружает базу данных.

{% endnote %}


## Синтаксис запроса {#id1FD86F7F}
```
http://passport.yandex.ru/
  ? mode=<mddomains>
```
### Параметры
#### mode
*Обязательный параметр*

## Формат ответа {#id0067AE5B}

Ответом является список доменов и их состояний (параметр `enabled`) в текстовом формате.

```no-highlight
okna.ru;enabled=1
bbb.ru;enabled=1
mellior.ru;enabled=1
mail.mellior.ru;enabled=1
mdelete.ru;enabled=1
eventtest.ru;enabled=1
dveri.ru;enabled=1
disables.ru;enabled=1
mike2.ru;enabled=1
zveri.ru;enabled=1
EOF!
```

Список завершается мнемоникой `EOF!`, даже если он пустой.

## Сообщения об ошибках {#id13BB6281}

При отсутствии прав доступа возвращается следующий ответ.

```no-highlight
ERROR! Acess denied
ERROR! Access denied for ip:95.108.175.188
EOF!
```

