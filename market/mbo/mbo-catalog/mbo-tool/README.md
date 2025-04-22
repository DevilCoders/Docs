# mbo-tool

Набор небольших Java программ для работы с нерегулярными и одноразовыми ручными задачами.

## Подготовка

Перед началом работы необходимо:

### 1. Копирование .postgres

Скопировать сертификат для postgres на aida с помощью команды: 

```shell
cd ~ && cp -r ../prediger/.postgresql/ .postgresql
```

## Как запустить в аиде или няне (новый метод)
Заливка куда угодно кроме аиды не работает, необходимо использовать старый метод описанный [тут](#запуск-в-nanny-с-помощью-gradle)

Для запуска надо вызвать скрипт `./scripts/dev/run-mbo-tool.py` и в --additional-parameters передать ему имя класса и другие параметры для запуска.

Пример:

```shell
./scripts/dev/run-mbo-tool.py --host <host> --additional-parameters DdlTool -t shops,good_shops
```

Для очистки после себя tail и прочих лишних процессов надо вызвать скрипт:
```shell
./scripts/dev/stop-mbo-tool.py --host <host>
```

Параметр host является не обязательным и по умолчанию равен aida.market.net
P.S. из-за устаревшей либы paramiko необходимо дождаться обновление библиотеки в арке https://a.yandex-team.ru/review/2227847/details, после обновления подключения к не aida должно заработать. 

## Запуск в Nanny с помощью gradle
Для запуска в Nanny надо вызвать специальный скрипт и передать ему имя тулы, аналогично запуску на aida.
По умолчанию запуск идет в тестинге.

Пример запуска в тестинге:
```shell
./scripts/nanny/run-tool.sh DdlTool -t shops,good_shops
```

Для запуска в Nanny в проде, необходимо передать продовый хост в параметре `--host`.

Пример запуска в проде:
```shell
./scripts/nanny/run-tool.sh --host production-market-mbo-tool-vla-1.vla.yp-c.yandex.net DdlTool -t shops,good_shops
```

Доступные тестовые инстансы:
```
testing-market-mbo-tool-sas-1.sas.yp-c.yandex.net
testing-market-mbo-tool-vla-1.vla.yp-c.yandex.net
```

Доступные продовые инстансы:
```
production-market-mbo-tool-sas-1.sas.yp-c.yandex.net
production-market-mbo-tool-vla-1.vla.yp-c.yandex.net
```

Хост по умолчанию:
```
testing-market-mbo-tool-vla-1.vla.yp-c.yandex.net
```

Пример запуска тулы:
```
./scripts/nanny/run-tool.sh --host production-market-mbo-tool-sas-1.sas.yp-c.yandex.net TestTool --hid 1010
```

Если для запуска тулы требуется файл, можно поступить следующим образом:
* Загружаем файл на инстанс:\
  HOSTNAME = sas3-7083-bd1-sas-market-prod--052-22848.gencfg-c.yandex.net\
  FILE_FROM = path/to/local/file.txt - требуемый файл\
  FILE_TO = path/to/remote/file.txt - файл на инстансе, в который будет скопировано содержимое file_from
```
./scripts/nanny/remote-data.sh --host HOSTNAME upload FILE_FROM FILE_TO
```

* Добавляем в код тулы флаг --file-path, принимающий путь к файлу на инстансе. Все загружаемые на инстанс файлы будут помещаться в директорию /data
* Запускаем тулу:\
  HOSTNAME = sas3-7083-bd1-sas-market-prod--052-22848.gencfg-c.yandex.net\
  FILE_PATH = data/FILE_TO - обязан начинаться с директории data/ + указанный вами путь к файлу на инстансе
```
./scripts/nanny/run-tool.sh --host HOSTNAME TestTool --file-path FILE_PATH --hid 1010
```

* Чтобы удалить ненужный файл на инстансе выполняем:
```
./scripts/nanny/remote-data.sh --host HOSTNAME remove FILE_PATH
```
Путь до логов:
```logs/mbo/$USER/logs```
Путь до компонента:
```logs/mbo/$USER/mbo-tool```

Что происходит в контейнере при запуске run-tool.sh:
1. Для каждого разработчика создается директория ```/logs/mbo/$USER/mbo-tool```
2. После локальной сборки собержимое папочки mbo/build/upload копируется в директорию пользователя
3. В контейнере запускается указанная в параментрах тула
3. При старте тулы (PID PORT USER), под которыми был совершен запуск, записывается в файл logs/mbo/mbo-tool.info, что позволяет отслеживать занимаемые порты и запущенные приложения

Важно:
* При каждом запуске run-tool.sh все файлы из вашей пользовательской директории, кроме /data, удаляются
* Логи лежат в директории ```/logs/mbo/$USER/logs``` и тоже очищаются перед каждом запуском run-tool.sh
* Окружение выбирается исходя из имени хоста (файла /etc/yandex/environment.type не существует в няне)

### Удаленный дебаг

В файле ./mbo-tool/src/main/properties.d/00_application.properties есть пропертя следующего содержания:
```
debug=-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:$DEBUG_PORT
```

Ставим `suspend=y`, чтобы после старта тулы jvm подождала подключения отладчика перед выполнением кода, и можно было цепляться к отладочному порту из идеи.
По дефолту это 87 (соседняя порпертя `debug.port` отвечает за что-то другое).
В случае чего какой порт слушает отладчик можно посмотреть в shell-логах (`logs/mbo/<username>/logs/mbo-tool.log.shell`).

java 11 не имеет возможности слушать отладчиком на ipv6 адресе, а только такой в няне и есть. Поэтому запускаем со специальной переменной для проброса порта, пример:
```shell
DEV_START_SSH_ARGS=-L1087:localhost:87 ./scripts/nanny/run-tool.sh --host sas3-7083-bd1-sas-market-prod--052-22848.gencfg-c.yandex.net TestTool --hid 1010
```
После такой команды можно будет подключиться в идее к localhost:1087 для отладки.
