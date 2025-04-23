## Описание продукта
https://wiki.yandex-team.ru/maps/dev/ui/products/constructor/

## NB

Конструктор - очень старый сервис, на старых технологиях.
Впероятно, у вас не получится собрать его локально.

Поднимите в [QYP](https://qyp.yandex-team.ru/) ubuntu-виртуалку и настройте
[arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide),
[docker](https://wiki.yandex-team.ru/qloud/docker-registry/?from=%2Fdocker%2F#kakustanovitdoker)
и [registry](https://wiki.yandex-team.ru/qloud/docker-registry/?from=%2Fdocker%2F#debian-basedubuntu)

```
npx qtools build -- --network=host
```


## Быстрый старт
```
git clone git@github.yandex-team.ru:maps/constructor.git ~/www/constructor
cd ~/www/constructor
make
docker-compose build front-constructor
docker-compose run -p "3000:8080" front-constructor
```

В браузере: `http://{username}.maps.dev.yandex.ru:3000/map-constructor/`.

Загрузка локалей
```
make i18n.get
```

## Тестирование
В проекте используются юнит-тестирование и интеграционное тестирование.
Первые проверяю результат работы конкретных функций, модулей (передали в функцию А -> получили Б).
Вторые проверяю логику работу приложения, как бы это делал пользователь (кликнули на кнопку -> появилось окно).
Юнит тесты запускаются автоматически по коммиту.
Интеграционные тесты необходимо запускать вручную перед сборкой пакета.
В будущем планируется запускать их автоматически при автоматической сборке пакета.

Для установки зависимостей интеграционных тестов пока требуется явно вызываи

### Команда для запуска юнит-тестирования
```
make unit-test
```

Клиентские тесты запускаются командой *test-client*. Тесты запускаются через технологии enb-bem-specs + phantomjs + mocha + sinon + expect.js
- enb-bem-specs - сборка специальных бандлов для проведения тестирования. Сборка происходит в папку *desktop.specs*
- phantomjs - браузер, который запускается через консоль.
- mocha - Синтаксический "каркас" тестов.
- expect.js - Вспомогательная библиотека для проверки результатов тестов.
- sinon - Библиотека для подмены серверных обращений.

**Манифест юнит-тестов:**
- Тесты автоматически запускаются при выполнении коммита. Нельзя коммитеть игнорирую тесты.
- Клиентский тест создается в той же папке, что и основной модуль. Название файла с постфиксом *.spec.js.
- Сам модуль должен называться modules.define('spec', ... Каждый тестовый модуль должен покрывать только свой модуль.
- В тестах можно использовать любые зависимости. Они не повляются на основной модуль.
- Каждый тест должен быть предельно простым. Лучше написать много мелких тестовы, чем один большой.
- Сетевые обращения должны быть подменены на клиенте. То есть тесты не должны зависеть от третьих сторон. Исключением является подгрузка модулей API Яндекс.Карт.  Пример теста с подмененными данными - rpc-client.
- В тестах не работает локализация. Если нужно проверить какое-то определенное значение, то библиотека локализации вернет значение keyset_key.
- Для дебага теста можно его запустить вручную из папки *desktop.specs*
- При ожидании промиса рекомендуется использовать конструкцию
```
makeAyns().then(function () {
    // test body
    done();
}).fail(done);
```

Запуск отдельных тестов происходит с добавлением параметра grep={Путь до теста}. К примеру,
```
make test-client grep=desktop.specs/rpc-client
```

### Команды для запуска интеграционного тестирования
```
make int-test-install
make int-test
```

## Deploying a release to testing

This project uses [qtools](https://github.yandex-team.ru/maps/qtools) to interface with docker, the
docker registry and the cloud platform Qloud.

### Release to testing

To upload static resources you must obtain `STATIC_CLIENT_KEY` from vault. Best tool for it is [ya](https://wiki.yandex-team.ru/yatool/).

To install `ya` use following snippet:
```sh
curl -k https://api-gotya.n.yandex-team.ru/ya > /usr/local/bin/ya
chmod +x /usr/local/bin/ya
```

```sh
make patch # or minor, major
STATIC_CLIENT_KEY=$(ya vault get version sec-01cjz2vkw9hqhf3c7skw5g4zxt -o STATIC_CLIENT_KEY) make release-testing
git push --follow-tags
```

### Deploy the current version to production

```sh
npx qtools deploy production
```
