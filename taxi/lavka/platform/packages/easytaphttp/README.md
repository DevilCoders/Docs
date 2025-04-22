# Фреймворк для тестирования ручек в TAP-формате

Тестируем wsgi приложения и прочее в стиле TAP/Mojo.

Запуск фреймворка:

```python
import easytap
import easytaphttp.wsgi

tap = easytap.Tap()

app = create_wsgi_app()

t = easytaphttp.wsgi.WSGITest(tap, app)

t.post_ok('/path/to/route', form={'a':'b'})
t.status_is(200)
t.json_is('foo.bar.baz', 42)

```

Для Flask есть упрощение:

```python

import easytaphttp.flask

t = easytaphttp.flask.FlaskTest(tap, 'module', 'app_instance')

```

Далее можем делать http-запросы-тесты.

Пример теста, тестирующего ручку:

```python
# выполняется запрос с отправкой данных формы
t.post_ok('/foo/bar', form={'a': 123, 'b': 'baz'})

# проверяется код ответа
t.status_is(200, 'Ответил без ошибки')

# проверяется тип ответа
t.content_type_is('application/json')

# некоторые проверки содержимого ответа
t.json_is('foo.bar.baz', [1, 2, 3], 'Список в foo.bar.baz правильный')

# можно на регенспы проверять
t.json_like('foo.bar.message', r'\sNot found', 'строка содержит текст')


```


```python

t.request_ok('get', '/user/123')
t.get_ok('/user/123')
t.post_ok('/user/123')
t.put_ok('/foo/bar', json={'a':'b'})
t.delete_ok('/baz', form={'login': 'test'})

```

При выполнении запросов мы можем заполнять формы, отправлять данные в виде json итп, например:

```python

t.post_ok('/user/123/save', form={'login': 'rsync', 'password': '123'})
t.post_ok('/user/123/save', json={'login': 'rsync', 'password': '123'})
t.post_ok('/user/123/save', data=json.dumps({'login': 'rsync', 'password': '123'}))

```

После того как запрос выполнен можем тестировать результаты ответа.

Тестировать в ответе можем:

1. xml (любые элементы по xpath)
2. json (любые элементы по jsonpath)
3. html (любые элементы по xpath)
4. заголовки ответа (любой заголовок + конкретно Content-Type)
5. коды ответа
6. ответ целиком

## Тесты ответа базис

* `t.status_is(code, desc)` - проверяет соответствие коду ответа
* `t.content_type_is(value, desc)` - проверяет значение Content-Type на точное соответствие
* `t.content_type_isnt(value, desc)` - инверсия предыдущей функции
* `t.content_type_like(regexp, desc)` - проверяет значение Content-Type на соответствие паттерну
* `t.content_type_unlike(regexp, desc)` - проверяет значение Content-Type на НЕсоответствие паттерну
* `t.content_type_like(regexp, desc)` - проверяет значение Content-Type на соответствие паттерну

## Тесты содержимого

* `content_is`, `content_isnt`, `content_like`, `content_unlike` - тестируют весь ответ на совпадение, несовпадение со значением или с паттерном;
* `json_is`, `json_isnt`, `json_like`, `json_unlike`, `json_has`, `json_hasht` - тестируют поля в json ответе на совпадение или несовпадение со значением или с паттерном, а так же на наличие или отсутствие;
* `xml_is`, `xml_isnt`, `xml_like`, `xml_unlike`, `xml_has`, `xml_hasht` - тестируют поля в xml ответе на совпадение или несовпадение со значением или с паттерном, а так же на наличие или отсутствие;
* `html_is`, `html_isnt`, `html_like`, `html_unlike`, `html_has`, `html_hasht` - тестируют поля в html ответе на совпадение или несовпадение со значением или с паттерном, а так же на наличие или отсутствие;



# Надстройка для flask

Упомянутая выше надстройка для flask помимо более простого конструирования еще умеет преобразовывать урлы используя flask'овый `url_for` для этого.

Например:

```

t = easytaphttp.flask.FlaskTest(tap, 'myappmodule', 'app')

# получить урл endpoint которого - foo
t.get_ok('foo')

# получить урл endpoint которого - /bar/<id>, заполнить id
t.get_ok(('bar', {'id': 123}), form={'baz': 123})

```

Так же 
