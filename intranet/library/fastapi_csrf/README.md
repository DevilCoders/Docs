## fastapi_csrf

Библиотека для генерации и валидации CSRF-токена в FastAPI приложениях

Алгоритмы для генерации и проверки токена реализованы согласно рекомендациям СИБ
https://wiki.yandex-team.ru/security/for/web-developers/csrf/#kakgenerirovatiproverjattoken

### Использование

Для использования нужно указать в ya.make проекта библотеку FastAPI
и путь к внутренней библиотеке fastapi_csrf

```
contrib/python/fastapi
intranet/library/fastapi_csrf/src
```

#### Добавление middleware

Для добавления валидации токена по умолчанию во все ручки нужно добавить middleware
в приложение FastAPI, а также добавить обработчик события startup для автоматического
обнаружения ручек, для которых валидация токена отключена (csrf_exempt)

```python
from fastapi import FastAPI
from intranet.library.fastapi_csrf.src import collect_csrf_exempt, CsrfMiddleware

app = FastAPI()

@app.on_event('startup')
async def collect_csrf_exempt_endpoints():
    await collect_csrf_exempt(app)

app.add_middleware(
    CsrfMiddleware,
    secret_key=settings.SECRET_KEY,
)
```

По умолчанию, токен будет браться из хедера `X-Csrf-Token`.
Если есть желание поменять название заголовка, то в middleware нужно передать аргументом новое
название хедера с помощью параметра `header_name`. Если же хочется, брать токен из куки - название
куки с помощью параметра `cookie_name`.
В случае передачи одновременно `cookie_name` и `header_name`, значение токена будет
получаться из куки.

Обязательно нужно передать secret_key приложения.

**Важно:** на момент выполнения CsrfMiddleware требует наличия в request.state атрибута user
с полем uid (обращение к `request.state.user.uid` не должно падать).
Самый простой способ добиться такого - выстроить порядок middleware так, чтобы сначала
была вызвана авторизационная middleware, которая и установит значение атрибута
`request.state.user`.

Пример:
```python
app.add_middleware(
    CsrfMiddleware,
    secret_key=settings.SECRET_KEY,
)
app.middleware('http')(middlewares.authentication)
```

*Примечание*: `middlewares.authentication` устанавливает значение атрибута `request.state.user`
до вызова следующей по стеку middleware.

Рекомендации СИБ по формату токена:
- задается в файле настроек
- в секретном ключе должны содержаться латинские буквы в нижнем и верхнем регистрах, цифры
- длина ключа — от 16 символов

#### Добавление исключений

В случае, если для ручки не должна быть вызвана проверка токена, можно использовать специальный
декоратор `@csrf_exempt` (по аналогии с django). Это допустимо делать для ручек, в которые никогда
не может придти обычный пользователь с фронтенда, а, например, соседний сервис.

Пример:
```python
from intranet.library.fastapi_csrf import csrf_exempt

# ...

@router.post('/endpoint')
@csrf_exempt
async def endpoint_handler(request: Request):
    ...
```
