## Запуск

Запускать `start.py` из `goals-status-mailing`.

Аргументы (обязательны все без значения по умолчанию):

`-e`, `--emails`: Список адресов получателей через пробел

`-s`, `--sender`: Email, с которого будет отправлен отчет

`-f`, `--from`: Дата начала отчета YYYY-mm-dd, включительно

`-t`, `--to`: Дата конца отчета YYYY-mm-dd, исключительно

`-d`, `--departments`: Список Id отделов на goals для составления отчета. Можно не указывать, если указаны `--goals`

 `-g`, `--goals`: Список Id отдельных целей, будут включены в начало отчета под заголовком "Отдельные цели". Можно не указывать, если указаны `--department`

 `-dump`, `--dump_report`: файл для сохранения репорта перед отправкой, по умолчанию не сохраняется

 `-i`, `--importance`: важность фильтруемых целей департаментов. По умолчанию: `1 2`

 `-lc`, `--long_comments`: флаг, отменяет сокращение комментария

 `-sc`, `--status_changes`: флаг, добавляет закрытые за выбранный период цели в отчет

Аргументы для авторизации:

`-sl`, `--smtp_login`: Логин для доступа к SMTP серверу, по умолчанию совпадает с `sender`

`-sp`, `--smtp_pass`: Пароль для доступа к SMTP серверу

`-at`, `--token`: универсальный токен доступа

`-gt`, `--goals_token`: токен доступа к goals, по умолчанию совпадает с `token`

`-ct`, `--charts_token`: токен доступа к charts, по умолчанию совпадает с `token`

## Запуск в Нирване

#### Подготовка

1) Создать virtual environment, добавить в него все необходимые пакеты.

    `pip install virtualenv`

    Из директории `goals-status-mailing`:

    `virtualenv venv`

    `source venv/bin/activate`

    `pip install -r requirements.txt`

2) В `venv/bin/activate` выставить `` VIRTUAL_ENV=`pwd` ``

3) Директории `mailing`, `templates`, `venv` положить в `.tar` архив

    `tar -czf mailing.tar mailing templates venv`

#### Создание кубика

1) Архив `.tar` зарузить в `job-binary-url`, __не в архивном режиме!__

2) В команде запуска сначала распаковать архив, включить окружение, затем выполнить скрипт.
Пример команды запуска:

```
bash -c 'tar -xzf ${param["job-binary-url"]} && \
source venv/bin/activate && \
python mailing/start.py \
-e ${param["emails"]} \
-s ${param["sender"]} \
-f ${param["from_date"]} \
-t ${param["to_date"]} \
-d ${param["goals-filter-ids"]} \
[#if param["smtp_login"]??]-sl ${param["smtp_login"]} [/#if] \
-sp "${param["smtp_pass"]}" \
[#if param["token"]??]-at ${param["token"]} [/#if] \
[#if param["goals_token"]??]-gt ${param["goals_token"]} [/#if] \
[#if param["charts_token"]??]-ct ${param["charts_token"]} [/#if]

