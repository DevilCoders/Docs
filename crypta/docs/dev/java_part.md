Разработка на Java
===================================================

2 основных проекта на java:
- [Crypta API](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/api)
- [Оффлайн склейка в CryptaID](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/ide) - метапроект, в который залинкованы релевантные.

Для того, чтобы собрать проект, нужно выполнить:
```ya ide idea  --iml-in-project-root -C crypta/api -r /your/path/to/idea/project```

P.S. После обновления репозитория нужно перезапускать эту команду, чтобы IDEA увидела изменения.

#### Поиск jdk
Используем аркадийный OpenJDK 17. Отличается от [официального релиза OpenJDK](https://jdk.java.net/17) наличием яндексовых сертификатов.
Нужную версию можно скачать из [Sandbox](https://sandbox.yandex-team.ru/resources?type=JAVA_JDK_ENVIRONMENT).

Сборка ```ya make```/```ya ide idea``` и так скачивает этот jdk, можно его найти в директории ```~/.ya``` так:\
```find ~/.ya -path "*/bin/java" -print -exec {} -version \;```

#### Конфигурация запуска
Полученный путь надо указать в idea, он будет выглядеть как-то так: `/Users/%USERNAME%/.ya/tools/v3/810389307`

Run -> Edit Configuration -> JRE -> ...

Дальше нужно будет через интерфейс натыкать путь до компилятора. На маках скрытые файлы (.ya) можно показать при помощи хоткея CMD + SHIFT + .

#### Особенности Java 17
В Java 11 ввели систему модулей (Jigsaw) и стало нужно явно указывать зависимости на "закрытые" внутренние пакеты JDK. В Java 17 запретили сборку c ```--relesase```, если всё еще есть зависимость на такие пакеты. Часть аркадийных библиотек всё ещё зависят от внутренностей JDK, поэтому в IDE нужно отключить сборку с ```--release```. Когда-то в будущем надо отказаться от таких зависимостей.
![d](https://jing.yandex-team.ru/files/artembelov/2022-04-06_17-44-02.png)

# Настройка окружения IDE для локального запуска и дебага API

После сборки проекта нужно настроить локальное окружение, чтобы API могло обращаться к сторонним сервисам с тестовыми криденшелами.

Для этого нужно создать конфигурацию проекта: `Run -> Edit Configurations...`

Добавляем новую конфигурацию, нажав на плюсик в левом верхнем углу окна настроек.

![add-new-configuration](https://jing.yandex-team.ru/files/unretrofied/Add_new_configuration.png)

Выбираем имя тестовой конфигурации, например `api-test`.

![configuration](https://jing.yandex-team.ru/files/unretrofied/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202021-06-24%2013-50-53.png)

Выбираем JDK (см. выше) и указаваем путь к классу `Main`, в нашем случае - `ru.yandex.crypta.api.Main`

В `-cp` записываем нужный модуль, в нашем случае это `api`.

Указываем рабочую директорию (`Working directory`) из шага про сборку проекта для IDE Idea - `/path/to/idea/project`, в
примере на скриншоте он лежит в домашней директории пользователя `unretrofied`: `/home/unretrofied/IdeaProjects/api4`.

В настройках переменных окружения (`Environment variables`) добавляем переменные тестового окружения.

![edit-env](https://jing.yandex-team.ru/files/unretrofied/Edit_env.png)

Тестовые пароли и токены хранятся в [yav](https://yav.yandex-team.ru).
Чтобы получить их и другие нужные перменные, достаточно запустить скрипт `crypta/api/get_environment.sh` со своим OAuth-токеном Sandbox. Токен нужен, чтобы скачать бинарник геодаты `geodata.bin`.

```bash
$ SANDBOX_OAUTH_TOKEN=AQAD-... ./get_environment.sh
Downloading https://proxy.sandbox.yandex-team.ru/2239919583 Downloading https://proxy.sandbox.yandex-team.ru/2239919583 [..] OK
Downloading https://proxy.sandbox.yandex-team.ru/2239918785 [..] OK
Downloading https://proxy.sandbox.yandex-team.ru/2239918785 [[.............................................................................................................................................................................................................................................] OK
.................] OK
--2021-06-24 14:07:11-- https://proxy.sandbox.yandex-team.ru/2253303309
Распознаётся proxy.sandbox.yandex-team.ru (proxy.sandbox.yandex-team.ru)… 2a02:6b8:0:3400::1:6, 5.255.240.6
Подключение к proxy.sandbox.yandex-team.ru (proxy.sandbox.yandex-team.ru)|2a02:6b8:0:3400::1:6|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 1751744739 (1,6G) [application/octet-stream]
Сохранение в: «geodata.bin»
geodata.bin                                        100%[================================================================================================================>]   1,63G  3,91MB/s    за 8m 26s

--2021-06-24 14:20:11-- (3,30 MB/s) - «geodata.bin» сохранён [1751744739/1751744739]

CRYPTA_ENVIRONMENT=testing
POSTGRES_CONNECTION_STRING=jdbc:postgresql://testing.database.crypta.yandex.net:6432/cryptadbtest?sslmode=require&ssl=true&prepareThreshold=0&socketTimeout=2&loginTimeout=1
POSTGRES_USERNAME=crypta
POSTGRES_PASSWORD=...
YT_PROXY=hahn.yt.yandex.net
YT_TOKEN=AQAD-...
AWAPS_PASSWORD=...
AWAPS_USER=robot-unicorn
SMTP_PASSWORD=...
SMTP_USER=robot-unicorn
BLACKBOX_URL=https://pass-test.yandex.ru/blackbox
SANDBOX_OAUTH_TOKEN=
SOLOMON_TOKEN=null
YQL_TOKEN=AQAD-...
YQL_USER=unretrofied
REACTOR_TOKEN=
S3_ACCESS_KEY_ID=...
S3_SECRET_KEY=...
TANKER_TOKEN=...
TVM_ID=2000761
TVM_SECRET=...
GEODATA=/home/unretrofied/arc/arcadia/crypta/api/geodata.bin
YT_RPC_USER=robot-crypta-testing
REDIS_SENTINELS=man-d1eye7ou5sdtj5v6.db.yandex.net:26379
REDIS_MASTERNAME=crypta_redis_test
REDIS_PASSWORD=...
DISABLE_IDM=yes
DISABLE_AUTH=yes
DISABLE_SCHEDULING=yes
DISABLE_TVM=yes
DEBUG_USER_NAME=unretrofied
```

В скрипте могут быть не все переменные, нужные вам, поэтому их нужно будет добавить самостоятельно.

Список переменных копируем в буфер обмена и вставляем в настройки IDEA.

![paste-env-vars](https://jing.yandex-team.ru/files/unretrofied/Paste_env.png)

![env-vars](https://jing.yandex-team.ru/files/unretrofied/Env_vars.png)

Всё сохраняем и запускаем API с созданным окружением: `Run -> Run...`, в появившемся окошке выбираем нашу конфигурацию.

Для дебага всё то же самое, но выбрать `Run -> Debug...`.
