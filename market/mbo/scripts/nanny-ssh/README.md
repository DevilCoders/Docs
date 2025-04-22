app_nanny.py - ssh утилита для няни
===============================================
```
usage: app_nanny.py [-h] [--data-centers [DATA_CENTERS [DATA_CENTERS ...]]]
                    [--prod] [--restart] [--grep GREP] [--tail TAIL]
                    [--thread-dump] [--command COMMAND] [--to-file]
                    [--ssh-link] service-name

Nanny services ssh util. Services:(mboc, mboc-tms, http-exporter, offers-api, card-api-cl, card-api-ag, flume-cl, flume-ag, flume-ui, flume-solr, lite, audit, react-ui, clab-ui, clab-api, clab-tms, alias-maker, alias-maker-meta, markup-worker, mdm, gwt, tms, gutgin-tms,
ag-api, mbo-ir-tms, mbo-classifier)

positional arguments:
  service-name

optional arguments:
  -h, --help            show this help message and exit
  --data-centers [DATA_CENTERS [DATA_CENTERS ...]], -dc [DATA_CENTERS [DATA_CENTERS ...]]
                        specific data centers
  --prod                run on prod
  --restart, -r         restart service
  --grep GREP, -g GREP  grep command
  --tail TAIL, -t TAIL  tail command
  --thread-dump, -td    get service thread dump
  --command COMMAND, -c COMMAND
                        run custom command
  --to-file, -tf        store to file instead of console
  --ssh-link            print ssh link to instances

```

Установка
---------
1. Установить третий питон (На mac os он автоматически, если вызвать `xcode-select --install`). Установить pip3 TODO написать как это сделать

Альтернативно можно просто поставить PyCharm (ключ вот тут https://wiki.yandex-team.ru/jetbrains/licenseservers/)  
и настроить третий питон и вирутальное окружение вот тут:  
File -> Settings -> Project: nanny-ssh -> Project Interpreter

2. cd <папка проекта>
3. python3 -m venv venv # создаем виртуальное окружение
4. source ./nanny-ssh/bin/activate # активируем виртуальное окружение
5. pip3 install -r requirements.txt # устанавливаем зависимости
6. `cp app.properties.sample app.properties` - создать app.properties по примеру app.properties.sample
(логин со стаффа и токен отсюда http://nanny.yandex-team.ru/ui/#/oauth/)

Запуск
------
1. source ./venv/bin/activate # активируем виртуальное окружение, нужно делать всякий раз при запуске
2. ./app_nanny.py ... # запускать с параметрами

Можно сделать alias и добавить его в ~/.bash_profile для мак или ~/.bashrc для линукса, чтобы запускать из любого места
```
alias app_nanny.py="source <dir>/venv/bin/activate && <dir>/app_nanny.py"
```

Конфиги
--------
В туле используются короткие алиасы наших проектов, посмотреть их можно в configuration.py

Примеры
--------
- Рестарт тестинга `./app_nanny.py flume-solr -r`
- grep логов прода `./app_nanny.py mboc --prod -g "Exception"`
- grep логов прода, захватывающий 1 строку до и 10 строк после: ./app_nanny.py mboc --prod --command "grep 'uploadMatrixAvailabilityExecutor job' logs/mboc-app/mbo-category.log -B 1 -A 10"
- tail логов прода `./app_nanny.py offers-api --prod -t -20`
- command `./app_nanny.py http-exporter -c "ps axu"`
- tail только из сасово и ивантеевки `./app_nanny.py flume-ui --prod -t -10 -dc iva sas`
- thread-dump в отдельные файлы (нужно создать папочку out) `./app_nanny.py mboc -tf -td`
- при использовании в -c %log% заменяется на путь до лог файла: `nanny mboc -c "tail -n 500 %log% | grep blabla"`

FAQ
--------
Q: Если появилась ошибка: `Authentication error while connecting to %s:%s - %s', 'iva1-5519.search.yandex.net', 10046, AuthenticationException('No authentication methods succeeded')`  
A: Попробуйте зайти на дев машинку и выйти. Например `ssh aida; exit;` и попробуйте снова.  
Если не получится, то вставьте в код строку `client = ParallelSSHClient(hosts=[instance], port=10046, pkey='~/.ssh/id_rsa', password='пароль',`

TODO
---------
- грепать другие файлы (сейчас можно через --command)
- поиск по архивным логам (нужна отдельная тула)
- грепать по конкретному хосту (сейчас можно только по дата-центру)
