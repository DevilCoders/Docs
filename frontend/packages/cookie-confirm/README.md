# cookie-confirm

Плашка о сборе кук, которая используются на разных сервисах Яндекса.
Есть несколько вариантов оборажения и 2 платформы - desktop/touch.

<img alt='Пример верстки' src='https://jing.yandex-team.ru/files/axaxaman/Снимок%20экрана%202020-02-26%20в%2021.21.00.png' >

## Разработка

```bash
#⠀Ставим зависимости
npm ci


# Запуск сборки примеров
npm run examples
http-server # или любой аналогичный веб-сервер
open http://127.0.0.1:8080/desktop.examples/cookie-confirm/bundle/bundle.html
# Теперь в браузере можно смотреть на разные сборки плашек и тестировать.

```

## Деплой

Плашка лежит на yastatic.net (https://yastatic.net/q/global-notifications/cc/_lego-cc.ru.js)

Для того, чтобы обновить плашку, надо загрузить результат сборки в этот репозиторий: https://github.yandex-team.ru/lego/lego-betastatic

В папку `public/cc` надо добавить новый код и расскатить.

## FAQ

Если при сборке падают ошибки вида `bem not found`,
вероятнее всего не слинкован пакет `islands-tools`.

Надо перейти в корень репозитория и написать `lerna link`.

## Обратная связь

Если у вас возникли проблемы или вопросы, то можно:

- Писать в [slack](https://lego-team.slack.com) (канал `support`).
- Создавать тикет в [startrek](https://st.yandex-team.ru/ISL) (очередь `ISL`).
