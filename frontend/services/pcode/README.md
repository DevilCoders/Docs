# Показывающий код [abc](https://abc.yandex-team.ru/services/pcode/)

### DEBUG

Для отладки сообщений kotik, можно экспортировать такую переменную `DEBUG`: `"*,-guard,-ipbus:*,-log4js:*,-express:*,log4js:main,-compression,-send"`

### Проверка изменений в коде сервера
В целом мануал не сильно отличается от описанного в arcadia/adv/pcode/web/pcode/docs/local-report-renderer.md

Глобальные переменные описанные в том мануале нужны и здесь.

Аналогично PCODE необходима переменная с портом для локального порта для RR: `LOCAL_RR_PORT`.
Её можно положить в [.env](https://github.com/motdotla/dotenv/blob/master/README.md) (нужно создать его, если он не существует. Пример в `.env.tpl`) файл - при запуске команд из инструкции ниже всё самостоятельно подтянется.
Можно аналогично прописать в переменные окружения.

**Алгоритм действий здесь следующий:**
1. Собираем локально renderer.js.
2. Подтягиваем с прода код с супербандлом.
3. Запускаем локальный RR, передаём ему путь до супербандла 
4. Поднимаем туннель

Если не сильно вникать в то, как всё устроено внутри, то со стороны это выглядит так:
Консоль 1, сборка и поднятие сервера:
```
yarn build && yarn local-rr
```
Консоль 2, запуск прокси:
```
yarn local-rr-tun
```

**Как понять что всё корректно запустилось и работает?**

Для проверки корректности работы вносим изменения в анонимку внутри getMain в файле server.ts:
![live-page](https://jing.yandex-team.ru/files/dimurer/manual_2022_05_06_004.png)

Сборка и поднятие сервера проходят успешно:

Собирается вебпак:
![live-page](https://jing.yandex-team.ru/files/dimurer/manual_2022_05_06_001.png)

Успешно загружается супербандл
![live-page](https://jing.yandex-team.ru/files/dimurer/manual_2022_05_06_002.png)

Версии из супербандла применяются
![live-page](https://jing.yandex-team.ru/files/dimurer/manual_2022_05_06_003.png)

Проверяем что при обработке сontext.js попадаем в наш код:
```
https://yandex.ru/ads/system/context.js?srcrwr=TEMPLATES:posts://dimurer-1000-ws1.tunneler-si.yandex.ru:443:5000&ssr-dev=1
```
Аналогичную проверку делаем для ручки `/meta/`. [Пример запроса](https://paste.yandex-team.ru/9248277). В консоли с поднятым сервером при каждом вызове должны падать сообщения.

