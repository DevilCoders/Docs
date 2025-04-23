## Расширения openapi

### `x-stall-permits`

Данную опцию можно указать как в общем уровне всего `yaml` так и на
уровне роута. Если указано и там и там, будут выполнены обе проверки.

```yaml

x-stall-permits:
    - auth_done
paths:
    /foo
        get:
            x-stall-permits:
                - foo
                - bar
            ...
```


Происходит следующее.

1. Собирается общий массив необходимых `permits`.
2. Определяется `cur_user` - текущий пользователь
   (если неавторизован - `guest`)
3. У пользователя вызывается `has_permit` с массивом пермитов
4. Возвращается 401 для пользователя `guest`, если `has_permit` вернул ложь
5. Для остальных ролей возвращается 403
6. Если всё успешно, то `cur_user` попадает в `request['stash']['cur_user']`


### `x-stall-over`

Позволяет предвыбрать и провалидировать значение до этапа исполнения.
Писать можно так же на уровне всей секции или роута.


```yaml
x-stall-over:
    - store:
        module: my.module.name1
        handle: handle
        path: foo.bar.store_id
paths:
    /foo
        get:
            x-stall-over:
                - order:
                    module: my.module.name2
                    handle: handle
                    path: foo.bar.order_id
                    args: 123
                ...
```

Происходит следующее

1. Собирается общий массив `overs` (сперва общие, потом роутные)
2. Каждый `over` исполняется:
 - по `path` ищется значение ключа во входном запросе, если его нет, сразу 403
 - найденный ключ передается обработчику (`my.module.name2.handle(key, args)`)
 - Обработчик должен вернуть объект (`not None`).
 - Этот объект попадёт в `request['stash']['$name']`
3. Если обработчик возвращает `None`, то возвращается 403


### `x-stall-middleware`

Позволяет подключить middleware к роутам описанным в данном файле yaml.

Действует на все роуты файла.

Применение директивы не в корне файла бессмысленно.


```yaml
x-stall-middleware:
  - foo.bar.baz.handlename
```

Даётся массив имён функций вместе с содержащими их модулями.

В примере - будет подгружен `foo.bar.baz` и в нём будет произведён поиск
функции с именем `handlename`. Эта функция будет использована как middleware.

Важно: `middleware` этого списка подключаются после всех middleware,
соответственно вызваны они будут до.


### `x-stall-prepare`

Выполняет преобразования с openapi ПЕРЕД обработкой.

```yaml
x-stall-prepare:
  remove_tail:
    - 'server.url': /baz

  append:
    - 'server.url': /foo/bar
  
  remove_head:
    - 'server.url': http://

  prepend:
    - 'server.url': https://

  append_keys:
    - 'routes.*': /baz
  prepend_keys:
    - 'routes.*': /v1/
```

### Запуск swagger

`make swagger-start`

Swagger будет доступен на http://localhost:8081/
 
 При добавлении нового yaml, его также надо добавить в `mk/frontend.mk` по аналогии с другими.


