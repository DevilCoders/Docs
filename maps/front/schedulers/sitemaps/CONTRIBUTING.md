# Contributing

## Как разрабатывать

Зависимости:
* [charles proxy server](https://www.charlesproxy.com/) нужен для разработки, чтобы работали http запросы использующие ipv6 адреса, т.к. docker внутри macOS не поддерживает ipv6.
* [ya](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup)
* [Docker](https://docs.docker.com) >= 20.10
* [Docker-Compose](https://docs.docker.com/compose/install/) >= 1.25
* make

Вся разработка происходит внутри docker контейнера в том числе и работа с arc.
Для сборки docker образа и установки зависимостей для разработки нужно выполнить команду: `make dev-setup`.
Далее нужно запустить `charles proxy server`, чтобы http запросы использующие ipv6 адреса работали внутри docker.
Затем необходимо запустить docker контейнер: `make dev` и можно приступать к разработке.
Для редактирования кода внутри запущенного контейнера можно использовать [VSCode](https://code.visualstudio.com/) и его расширение [Remote - Containers](https://code.visualstudio.com/docs/remote/containers-tutorial#_install-the-extension), подключаемся к запущенному контейнеру VSCode-командой `Remote-Containers: Attach to Running Container...`.
В качестве домашней директории внутри контейнера используются named volume, поэтому изменения внутри неё сохранются даже после пересоздания конетйнера.

```
arc mount -m ~/arcadia -S ~/store
cd arcadia/maps/front/schedulers/sitemaps/
make dev-setup
make dev

# Устанавливаем зависимости внутри контейнера
make deps

# Начинаем разработку, например:
GENERATOR=orgs make generator
```

### Токены и Доступы
* Получить YQL_TOKEN можно [здесь](https://yql.yandex-team.ru/oauth)
* Получить YT_TOKEN см. [инструкцию](https://wiki.yandex-team.ru/yt/gettingstarted/#tokendostupa)
* S3-MDS(testing)
    - [Доступы](https://idm.yandex-team.ru/system/s3-mds-test/roles#rf=1,rf-role=tlfYdI3e#s3-mds-test/maps-front-maps-sitemap-2644-92890/service-account-role/writer,f-status=all,f-role=s3-mds-test,sort-by=-updated,rf-expanded=tlfYdI3e).
    - Токены необходимо получить для сервиса [maps-front-maps-sitemap](https://abc.yandex-team.ru/services/maps-front-maps-sitemap/), см. [инструкцию](https://wiki.yandex-team.ru/mds/s3-api/authorization/#upravlenieaccesskeys). Полученные токены можно сохранить в ~/.bash_profile под именами `SITEMAPS_TESTING_AWS_ACCESS_KEY_ID` и `SITEMAPS_TESTING_AWS_SECRET_ACCESS_KEY`.
    - В тестинге есть два бакета: `s3-maps-front-sitemaps` и `s3-maps-front-sitemaps-test`. Их можно использовать для разработки.

### S3. Структура файлов внутри бакета
**Внимание !!!** При изменении структуры файлов внутри бакета также необходимо изменить nginx [конфиг](https://github.yandex-team.ru/maps/maps/blob/dev/tools/configs/nginx/extension.conf) внутри Веб-карт, если это нужно. Чтобы робот шёл по нужному пути.

### Переменные окружения внутри приложения

Ниже представлены все переменные окружения, которые используются внутри nodejs.
| Имя | Значение | Описание |
| - | - | - |
| `GENERATOR` | `"masstransit" or "orgs" or "regions" or "houses"` | Указывает какой генератор запускать |
| `OUT_DIR` | `string` | Путь к папке куда nodejs процесс сможет сохранить результаты своей работы |
| `YQL_TOKEN` | `string` | Токен для [YQL](https://yql.yandex-team.ru/docs/yt/interfaces/cli#autentifikaciya) |
| `YT_TOKEN` | `string` | Токен для [YT](https://wiki.yandex-team.ru/yt/gettingstarted/#tokendostupa) |
| `GEOBASE_DATA_BIN_PATH` | `string` | Путь до [бинарных данных](https://wiki.yandex-team.ru/geotargeting/libgeobase/#geodata6.bin1.6gb) для геобазы |
| `HTTP_PROXY` | `string` | http прокси нужен только для разработки, чтобы работали http запросы использующие ipv6 адреса внутри docker на macOS |
| `BUCKET` | `string` | Название S3 бакета |
| `AWS_ACCESS_KEY_ID` | `string` | Id ключа доступа для S3 |
| `AWS_SECRET_ACCESS_KEY` | `string` | Ключ доступа для S3 |
| `AWS_END_POINT` | `"http://s3.mdst.yandex.net" or "http://s3.mds.yandex.net"` | |

### Может пригодиться

#### S3. Просмотр

Посмотреть что хранится внутри S3 бакета можно с помощью одного из [клиентов](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/), например [aws](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#awscommandlineinterface):
```
AWS_ACCESS_KEY_ID=<id ключа> AWS_SECRET_ACCESS_KEY=<ключ доступа> aws --endpoint-url=http://s3.mdst.yandex.net s3 ls
```
или воспользоваться клиентом под MacOs [Cyberduck](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#cyberduckgui)(GUI)

#### Отладка VSCode

Поставить плагин `ms-azuretools.vscode-docker`.
Запустить `NODE_FLAGS="--inspect-brk=0.0.0.0:9229" GENERATOR=houses make generator`, nodejs процесс начнёт выполнять код только после того, как к нему будет присоединён отладчик. Для этого нужно зайти в отладчик и нажать кнопку RUN, смотри скриншот:
![Запуск отладчика](https://jing.yandex-team.ru/files/reshetnev-gb/sitemaps-debugger.jpeg)
