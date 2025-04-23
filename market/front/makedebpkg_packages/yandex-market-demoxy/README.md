yandex-market-demoxy
----------------

Web сервис. Служит для запуска заранее сконфиигурированных процессов на сервере, где он сам крутится. Логика такова:
  - Пришел запрос на foo.yandex.ru/bundles/index/_index.css(мы заранее настроили перенаправление всех запросов за *.css в demoxy)
  - Demoxy получил этот запрос
  - Проверил, есть ли в его конфиге включенные проекты, которые регекспом матчатся на host+url, который ему пришел
  - Если есть и процесс, описанные в конфиге ещё не запущены, то делаем это
  - Отдаём запрос в сокет, который указан в конфиге demoxy
  - Возвращаем ответ клиенту

Получить информацию о том что эта штука умеет можно из [TODO][todo-list] разработчика.

### TODO по пакету

  - [ ] Узнать у админов, как мне это мониторить на разработческих серверах
        меня интересует есть ли там monrun и если нет, то насколько будет им сложно его туда поставить и как я буду узнавать о проблемах, возможно стоит сделать мониторинг на основе jenkins, это будет очень просто, потому что demoxy отдаёт свои заголовки для обработанных запросов и умеет кидать 500 ошибки когда что-то идёт не так.

### Особенности

  - Работает от рута, потому что я ещё не придумал хорошего способа разделения привилегий
  - Написана на golang
  - Golang выкачивается и компилируется при сборке пакета из-за того что в репозиториях убунты лежат очень старые пакеты
  - Конфиг с маркетными проектами едет в репозитории(там пока нет ни одного реального проекта, тулза в стадии разработки)

### Сборка пакета

Если вы пересобираете пакет, то скорее всего вашей целью является сборка пакета с новой версией demoxy.

Чтобы собрать пакет со свежей версией нужно посмотреть последний тэг на [github][tags-link] и подставить его в `_ver` внутри `PKGBUILD`:
```bash
_ver=1.0-alpha1
```

После этого самостоятельно выкачать этот архив и посчитать его sha256 контрольную сумму:
```
$ wget https://github.com/corpix/demoxy/archive/1.0-alpha1.tar.gz
--2015-05-29 18:12:52--  https://github.com/corpix/demoxy/archive/1.0-alpha1.tar.gz
Resolving github.com (github.com)... 192.30.252.131
Connecting to github.com (github.com)|192.30.252.131|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://codeload.github.com/corpix/demoxy/tar.gz/1.0-alpha1 [following]
--2015-05-29 18:12:52--  https://codeload.github.com/corpix/demoxy/tar.gz/1.0-alpha1
Resolving codeload.github.com (codeload.github.com)... 192.30.252.146
Connecting to codeload.github.com (codeload.github.com)|192.30.252.146|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [application/x-gzip]
Saving to: `1.0-alpha1.tar.gz'

    [ <=>                                                                                      ] 6,468       --.-K/s   in 0s

2015-05-29 18:12:53 (69.6 MB/s) - `1.0-alpha1.tar.gz' saved [6468]

$ sha256sum 1.0-alpha1.tar.gz
3a35f0ac4be3a926d36be80c42c97e2a331317c3c41acf4893d70287aab22b48  1.0-alpha1.tar.gz
```

Контрольную сумму необходимо подставить в соответствующую переменную в PKGBUILD.

В остальном, к этому пакету применимы [общие инструкции по сборке](https://github.yandex-team.ru/market/packages#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2).

###Загрузка в репозиторий

Этот пакет нужно загрузить в репозиторий [market-amd64](https://github.yandex-team.ru/market/packages/blob/master/README.md#market-amd64).

Информация о том [как загружать пакеты](https://github.yandex-team.ru/market/packages/blob/master/README.md#%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9).

[tags-link]: https://github.yandex-team.ru/market/demoxy/releases
[todo-list]: https://github.com/corpix/demoxy/blob/master/TODO.org
