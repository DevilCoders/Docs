# debug proxy

## фичи

- можно смотреть запросы из приложения в бэкенды
- можно смотреть запросы из приложения в кадавр при запуске тестов и не только
- можно смотреть создание сессий и установку стейта из тестов в кадавр
- можно подменять тело ответов, заголовки и т.д.

сам дебаг прокси https://github.com/avwo/whistle
(минус только в том что основная дока на китайском: http://wproxy.org/whistle/)

по вопросам и предложениям => [asvasilenko@](https://staff.yandex-team.ru/asvasilenko) или [abiryukov@](https://staff.yandex-team.ru/abiryukov)

## usage

- склонировать кадавр на логрус

```
git clone git@github.yandex-team.ru:market/kadavrique.git ~/kadavrique && \
cd ~/kadavrique && \
veendor install
```


- запустить кадавр с опциями `--proxy-port, --ui-port, --log-level debug`

```
$ npm start -- --port 8089 --proxy-port 9090 --ui-port 9091 --log-level debug

Kadavr INFO debug proxy listen on null:9090
Kadavr INFO debug proxy UI  listen  on null:9091
Kadavr INFO


        open UI: http://logrus02vd.market.yandex.net:9091#network


        // в приложении нужно установить кук
        document.cookie = 'kadavr_session_id=debug_proxy;  path=/';

        // удалить эту куку
        document.cookie = 'kadavr_session_id=debug_proxy; expires=' + (new Date()).toGMTString() + '; path=/';



Kadavr INFO Server is listening on :::8089 (IPv6)
```

- открыть ссылку из консоли `open UI: http://logrus02vd.market.yandex.net:9091#network`
- открыть proxy UI
- запустить приложение и указать прокси через переменные окружения KADAVR_HOST, KADAVR_PORT

```
$ KADAVR_HOST=localhost KADAVR_PORT=9090 make rebundle
```


- установить куку в браузере для приложения `document.cookie = 'kadavr_session_id=debug_proxy;  path=/';`
- теперь c установленной кукой все запросы в бэкенды приложение будет отправлять в кадавр, а там их ждет наш прокси 0_0
- в proxy UI при загрузке страниц видим все запросы в бэкенды


## usage с тестами

При запуске тестов будем видеть запросы из приложения в кадавр, если в ginny.conf указать логрус

Если нужно смотреть запросы из автотестов в кадавр (создание сессий, установка стейта), тогда при запуске автотестов нужно тоже указать KADAVR_HOST, KADAVR_PORT

```
$ KADAVR=1 KADAVR_HOST=logrus02vd.market.yandex.net KADAVR_PORT=9090 make autotest
```

`KADAVR_PORT=9090` - это порт debug-прокси
