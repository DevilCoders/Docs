## rex (Reliable EXternally)

rex - это прототип инструмента внешнего мониторинга.


### Как это рабает

TODO


### Секреты

Хранятся на
[вики](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/rex/secrets/)
(доступ ограничен). Ответственные talion@, koorgoo@, dhmax@.


### Антиробот

Чтобы получать оригинальные странички, rex необходимо обходить редиректы на
каптчу от [Антиробота](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/AntirobotOnline/).
Есть механизм, чтобы избежать таких редиректов, для их работы необходимо знать
иметь __справки__, значения специально куки, чтобы Антиробот пропускал запрос.


#### Сколько справок нужно?

Метрики говорят, что в среднем нужна 1 справка на 12-13 запросов.


#### Как получать справки?

Для начала нужно знать адреса антироботных хостов. Это можно сделать с помощь `sky` утилиты:

```bash
$ sky list G@ALL_ANTIROBOT
```

А вот порт на хостах зависит от топологии. Самый верный способ - подсмотреть в сервисе
[production_antirobot_iss](https://nanny.yandex-team.ru/ui/#/services/catalog/production_antirobot_iss/).
На момент написания документации порт `13512`.

Когда всё известно, остается получить N справок и указать файл в `rex.yml`. Однако, сделать это можно
только с хостов, которые входят в макрос [martyrs](https://c.yandex-team.ru/groups/martyrs) (с них есть
дырка до Антиробота).

Пример получения 10 справок:

```bash
$ http --output spravkas.txt "http://sas1-2658.search.yandex.net:13512/admin?action=getspravka&count=10"
```

Подсказка: [HTTPie](https://httpie.org/doc#installation) можно заменить на cURL.


### Contributing

#### Требования

- Go 1.10+
- Ansible 2.6+

Подсказка: используй [Homebrew](https://brew.sh) (+ Cask) на macOS.


#### Первые шаги

Сделай checkout репозитория:

```
$ cd $GOPATH
$ git clone git@bb.yandex-team.ru:searchmon/rex.git
$ cd rex
```

Запусти rex:

```
$ go install . && rex
```

Подсказка: Чтобы `rex` команда была доступна, нужно чтобы `$GOPATH/bin` был
в твоём `$PATH`.
