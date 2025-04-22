# **Prostarter (process starter)**
### **About**
prostarter - утилита для стандартизации запуска сервисов внутри различных облаков. Стартер получает информацию о облаке и передает ее сервис с помощью переменых окружения.
### **How to use**
prostarter принимает первым аргументом бинарь который надо запустить, можно задать полный путь или имя которое резолвится через PATH. Все остальные аргументы будут переданы при запуске бинаря как есть.
Пример:
```shell script
prostarter nginx -c /etc/nginx/nginx.conf
```
### **Exported environment variables**
Переменные окружения которые проставляет prostarter:
* `PROSTARTER_IS_STARTER` - со значением `true` означает что просес запущен под стартером
* `PROSTARTER_CPUMILS_LIMIT` - лимит использования cpu ресурсов в miliCPU (1000 ~ 1 ядро), точное число
* `PROSTARTER_CPUMILS_GUARANTEE` - гарантированая квота использования cpu в miliCPU, точное число
* `PROSTARTER_CPUCORES_LIMIT` - лимит использования cpu в ядрах (CPUMILS_LIMIT округленный в меньшеую стороно, но не меньше 1)
* `PROSTARTER_CPUCORES_GUARANTEE` - гарантированая квота использования cpu в ядрах (CPUMILS_GUARANTEE округленный в меньшеую стороно, но не меньше 1)
* `PROSTARTER_MEMORY_LIMIT` - лимит использования памятив байтах
* `PROSTARTER_MEMORY_GUARANTEE` - гарантированый объем памяти в байтах
* `PROSTARTER_CONFIG_PATH` - путь до файла конфигурации сервиса
* `PROSTARTER_LOG_PATH` - дериктория для логов сервиса
* `PROSTARTER_LOG_FILE` - путь до основного лог файла сервиса
* `PROSTARTER_ROOT_PATH` - путь до каталога в котором должно работать приложения или же рабочий каталог
* `PROSTARTER_PERSISTENTDATA_PATH` - путь по которому **может** быть смантирован каталог который гарантировано не затирается после пересоздания контейнера в облаке (правда содержание каталога может быть утерено в некоторых других случаях, т.е. важную информацию хранить в этом каталоге нельзя)
* `PROSTARTER_DATAGETTER_PATH` - путь по которому надодятся данные из data-getter
* `PROSTARTER_TEMP_PATH` - каталог предусмотренный для создания временных файлов, автоматически не чистится, но чистится при пересоздании контейнера
* `PROSTARTER_DC` - датацентр в котором запущен контейнер
* `PROSTARTER_ENV` - environment в котором запущен контейнер (production/testing....)
* `PROSTARTER_LISTEN_HOST` - хост на котором должен слушать сервис
* `PROSTARTER_LISTEN_WEB_PORT` - http порт контейнера (чаще всего в наших контейнерах на этом порту слушет nginx)
* `PROSTARTER_LISTEN_WEB_SSL_PORT` - https порт  контейнера (такое же правило с nginx как и в случае http)
* `PROSTARTER_LISTEN_APP_PORT` - порт на котором должен слушать сервис чтобы принимать запросы спроксированые через nginx
* `PROSTARTER_LISTEN_GRPC_PORT` - grpc порт (не ssl) на котором в зависимости от конфигурации может слушать сервис или nginx
* `PROSTARTER_LISTEN_GRPC_SSL_PORT` - grpcs порт (ssl), аналогично grpc порту
* `PROSTARTER_LISTEN_GRPC_APP_PORT` - grpc порт на котором должен слушать сервис если grpc/grpcs запросы проксирует nginx
* `PROSTARTER_LISTEN_DEBUG_PORT` - порт на котором могут слушать дебаг тулзы сервиса
* `PROSTARTER_VOLUMES` - json хеш с информацией о всех вольюмах подключеных к контейнеру где ключ это моунт пойнт вольюма, а значение имеет вид `{"mountPoint":"/something","quota":"квота в байтах"}`
* `PROSTARTER_LABEL_*` - labels сервиса, имя label приведется к верхнему регистру, - заменится на _ и добавится префикс PROSTARTER_LABEL_, пока что работает только в deploy
### **Accepted environment variables**
Переменные окружения которые принимает prostarter в качстве конфигурации
* `PROSTARTER_NAME` - имя сервиса, если отличается от имени бинаря
* `PROSTARTER_PODAGENT` - юрл адрес на котором слушает podagent (deploy), по умолчанию `http://127.0.0.1:1/`
* `PROSTARTER_DUMPJSON` - путь до dump.json внутри nanny контейнера, по умолчанию `${pwd}/dump.json`
* `PROSTARTER_CONTAINERROOT` - рутовой путь внутри nanny контейнера, используется для тестов, по умолчанию `/`
* `PROSTARTER_COMP` - включает речим совместимости со старым стартером (just starter), об этом ниже
### **Starter compatibility**
Режим совместимости со starter (прошлый подход к подобной утилите)
Если `PROSTARTER_COMP` выставлен в один из указаных ниже вариантов, то в запускаймый бинарь дополнительно будут переданны указанные аргументы, в остальном функционал не меняется:
* `JAVA` будут переданны следующие аргументы:
    - `--logdir=` со значением из `PROSTARTER_LOG_PATH`
    - `--httpport=` со значением из `PROSTARTER_LISTEN_APP_PORT`
    - `--debugport=` со значением из `PROSTARTER_LISTEN_DEBUG_PORT`
    - `--tmpdir=` со значением из `PROSTARTER_TEMP_PATH`
    - `--datadir=` со значением из `PROSTARTER_DATAGETTER_PATH`
    - `--extdatadir=` со значением из `PROSTARTER_PERSISTENTDATA_PATH`
    - `--environment=` со значением из `PROSTARTER_ENV`
    - `--dc=` со значением из `PROSTARTER_DC`
    - `--cpu-count=` со значением из `PROSTARTER_CPUCORES_GUARANTEE`
* `CPP` будут переданны следующие аргументы:
    - `--config=` со значением из `PROSTARTER_CONFIG_PATH`
    - `--host=` со значением из `PROSTARTER_LISTEN_HOST`
    - `--port=` со значением из `PROSTARTER_LISTEN_APP_PORT`
    - `--log-path=` со значением из `PROSTARTER_LOG_FILE`
    - `--dc=` со значением из `PROSTARTER_DC`
    - `--env=` со значением из `PROSTARTER_ENV`
    - `--root-path=` со значением из `PROSTARTER_ROOT_PATH`
    - `--listen-threads=` со значением из `PROSTARTER_CPUCORES_GUARANTEE`
* `PYTHON` будут переданны следующие аргументы:
    - `--config=` со значением из `PROSTARTER_CONFIG_PATH`
    - `--host=` со значением из `PROSTARTER_LISTEN_HOST`
    - `--port=` со значением из `PROSTARTER_LISTEN_APP_PORT`
    - `--log-path=` со значением из `PROSTARTER_LOG_FILE`
    - `--dc=` со значением из `PROSTARTER_DC`
    - `--env=` со значением из `PROSTARTER_ENV`
    - `--root-path=` со значением из `PROSTARTER_ROOT_PATH`
    - `--listen-threads=` со значением из `PROSTARTER_CPUCORES_GUARANTEE`

Пример:
```shell script
user@localhost:/tmp$ PROSTARTER_COMP=JAVA prostarter echo --test var --or something
--logdir=/tmp/logs/echo --httpport=8081 --debugport=8282 --tmpdir=/tmp/tmp --datadir=/tmp/data-getter --extdatadir=/tmp/echo --environment=testing --dc=sas --cpu-count=8 --test var --or something
```


### **Development**
Информация о том как запустить prostarter для каких либо экспериментов
#### **Nanny**
Выставить необходимые переменые окружения:
```shell script
source dev/nanny.sh
```
Информацию о _контейнере_ можно поправить в `dev/dump.json`
#### **Deploy**
Выставить необходимые переменые окружения:
```shell script
source dev/deploy.sh
```
запустить эмулятор podagent
```shell script
python3 dev/podagent.py &
```
Информацию о _контейнере_ можно поправить в `dev/podagent.json`
