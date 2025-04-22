# Static in S3

Позволяет загрузить вашу статику в общий карточный бакет (`front-maps-static`) в S3.

## Загрузка файла

Итоговый урл файла будет выглядеть так: `https://yastatic.net/s3/front-maps-static/${project}/${path}`. Параметры смотрите ниже.

**Важно**: Для проектов, использующих `qtools`, используйте команду [`upload-static`](https://a.yandex-team.ru/arcadia/maps/front/packages/qtools/docs/geo-specific.md#upload-static).

**Адрес**: `/static/upload-file`

**Метод**: `PUT`

**Параметры**:

* `project` — название ваша проекта, будет использоваться в урле.
* `path` — путь до файла.
* `key` — ключ для загрузки. Для получения ключа пишите [@alt-j](https://staff.yandex-team.ru/alt-j) или [@sigorilla](https://staff.yandex-team.ru/sigorilla). Если вы используете Trendbox CI, то ключ доступен в переменной окружения `STATIC_CLIENT_KEY`.
* `bucket` — бакет, в который грузим файл. По умолчанию, `front-maps-static`.

## Проверка на существование файла в бакете

**Адрес**: `/static/is-file-exists`

**Метод**: `GET`

**Параметры**:

* `project` — название вашего проекта.
* `path` — путь до файла.
* `bucket` — бакет, в котором будет проверяться наличие файла. По умолчанию, `front-maps-static`.
