Вёрстка паспорта
================

> Пакет yandex-passport-frontend

## Разработка

### Доступы
* Попросить у yakushevsky@ доступ в https://abc.yandex-team.ru/services/passport-frontend/

### Окружение
Далее на `python-dev2.passport.yandex.net`:
```bash
$ git clone git@github.yandex-team.ru:passport-frontend/core.git
$ cd core

$ NODE_OPTIONS="--max_old_space_size=4096" make
$ npm config set yandex-passport-frontend:port NNNN
$  make start
```
Теперь можно перейти на `https://NNNN.passportdev.yandex.ru/auth/`

## Сборка следующей версии

```bash
$ npm run changelog
$ # лог изменений с последней сборки
```

```bash
$ dch -i
$ # меняем версию, добавляем лог изменений
$ npm run release
```

## Добавление новой страницы

Чтобы добавить страницу `pagename` выполните:
```bash
$ make pages/pagename
```

Это команда создаст дефолтные файлы, которые вы сможете расширить по вашему желанию:
```bash
$ ls pages/pagename
pagename.js pagename.styl pagename.yate
```

Чтобы увидеть вашу новую страницу, перейдите по ссылке:
```
http://N.passportdev.yandex.ru/registration/simple/?_page=pagename
```

Чтобы добавить продакшн `url` для вашей новой страницы, обратитесь к `ppokrovsky@`.

## Локальный дев

Сначала делаем

```
make local-dev
```

Это команда скачает сертификат, и tvm тикет

В терминале держим открытую вкладку с 
```
ssh -L 127.0.0.1:8080:passport-test-internal.yandex.ru:80 python-dev2.passport.yandex.net
```

Это нужно чтобы пробросить порт. В другой вкладке 

```
npm run local
```

Предварительно единожды нужно установить [magicdev](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/magicdev),  поправить ~/.tvm.json

```
# ~/.tvm.json 

{
    "clients": {
        "passport": {
            "secret": "SECRET KEY (есть в твм тикете)",
            "self_tvm_id": 2010644,
            "dsts": {
                "cloud": {
                    "dst_id": 2000060
                },
                "afisha": {
                    "dst_id": 2001171
                },
                "addrs-search": {
                    "dst_id": 2008261
                },
                "blackbox": {
                    "dst_id": 224
                },
                "mimino": {
                    "dst_id": 239
                }
            }
        }
    }
}
``` 

и в /etc/hosts прописать:

```
127.0.0.1   passport-test-internal.yandex.ru
```

Инстанс будет доступен по адресу

```
https://localhost.msup.yandex.ru/auth
```

## Тестирование

### Hermione

Перед запуском тестов нужно поднять tvmtool для получения TVM-тикетов для тестовых запросов в бекенд:

```
npm run tests-tvm
```

Запуск тестов:

```
npm run hermione
```

Запуск конкретного теста:

```
npm run hermione -- --grep 'название теста'
```

Запуск конкретного теста в режиме отладки:

```
TODO
```

Построение отчёта о прохождении тестов:

```
TODO
```

#### Окружения для запуска тестов

## Технические подробности

### Технологии

[Node.js](http://nodejs.org/docs/v0.8.23/api/), [express](http://expressjs.com/api.html)
, [jquery](http://api.jquery.com/), [yate](https://github.com/pasaran/yate)

### Ограничения

- [Правила работы с git](http://doc.yandex-team.ru/Mail/dev-interface-guide/concepts/general.xml#dev-cycle)
- [Code style](https://github.yandex-team.ru/Daria/codestyle)

### Тезисы

- должно работать с выключенным JS
- легко добавлять новые страницы
- страницы строятся из блоков
- страницы не зависят друг от друга

### Структура проекта

### Алгоритм рендеринга страницы

1. Любая страница регистрации строится на основе [JSON-шаблона](lib/passport-form/template.js) (JSON c описанием доступных контролов и их свойств).
2. JSON-шаблон [обрабатывается на сервере](lib/passport-form/index.js), к нему могу добавиться ошибки и значение
3. На JSON-шаблон накладывается YATE-шаблон страницы
