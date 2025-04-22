# Беты Директа: создание и управление

## Пререквезиты { #prerequisites }

1. ssh на ppcdev, членство в группе ppc. 
Для разработчиков Директа по abc это должно появляться автоматически. 
2. Для arc-бет: настроить oauth-токен для arc [по инструкции](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

## Общая информация

Беты запускаются на ppcdev-ах. 
Если не оговаривается другое, все команды подразумеваются на ppcdev. 

Беты можно делать на основе рабочих копий от разных vcs. 
В зависимости от vcs одни и те же действия могут выполняться по-разному.

На бетах по умолчанию есть только рабочая копия perl. Другие сервисы используются из общих инсталяций.
При необходимости можно запустить на бете и другие сервисы. Например: java-сервисы, dna. Про работу с сервисами смотри отдельные секции ниже.

## Резервирование портов под беты { #beta-ports }

- порты выделяются программой `beta-ports.pl`  
(запускать на том ppcdev, где хочешь выделить порты)
- справка: `beta-ports.pl -h`
- посмотреть свободные порты: `beta-ports.pl -a`
- зарезервировать один порт (порт выбрать из предыдущего пункта):  
`beta-ports.pl alloc -p <номер свободного порта>`
- зарезервировать K портов начиная с номера S:  
`beta-ports.pl alloc -s S -n K` 


## Svn-беты { #svn }

### Создание svn-беты

Создать бету из транка:
```
direct-create-beta
```

При создании возможно указать порт (свободный из зарезервированных) и [perl-бранч](https://a.yandex-team.ru/arc/branches/direct/perl), который будет использовать бета:
```
direct-create-beta -p <port> -b <branch>
```

### Обновление svn-беты

Обновить бету до текущего транка (в том числе будут обновлены java-сервисы и dna):
```
direct-mk up
```

Либо, можно обновить бету на нужную ревизию вручную:
```
svn up -r <revision>
direct-mk beta-postupdate
``` 

### Удаление svn-беты

```
direct-delete-beta /var/www/beta.yourlogin.12345
```

## Arc-беты { #arc }

{% note alert %}

Беты на arc существуют в экспериментальном режиме, возможны странности и баги.

Фидбек можно писать в тикет <https://st.yandex-team.ru/DIRECT-143926>.

{% endnote %}

Преимущества arc-бет:
- Запуск java-сервисов на бетах происходит быстрее, за счет быстрого создания рабочей копии.
- Можно использовать arc-бранчи или `arc sync`, для разработки и дебага на бете.

Особенности:
- Для perl и java-сервисов используется единая рабочая копия.
- Директория c perl сервисами &mdash; `arcadia/direct/perl`, а не корень беты.

Недостатки:
- Исторически, разработка происходит в svn, поэтому на arc-бетах могут быть поддержаны не все сценарии работы с бетой.

### Создание arc-беты

Для использования arc-бет необходимо настроить oauth-токен для arc [по инструкции](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

Создать бету из транка:
```
direct-create-beta --arc
```

Создание беты из бранча пока не поддержано. Выбрать бранч можно после создания беты.

### Обновление arc-беты

Работа с репозиторием выполняется из директории `arcadia`. Общую информацию про работу с arc можно прочитать в [документации arc](https://docs.yandex-team.ru/arc/).

Обновить рабочую копию до нужного состояния:
- `arc pull` &mdash; обновить локальную ветку изменениями из удаленной ветки.
- `arc checkout <branch>` &mdash; переключиться на ветку `branch`.
- `arc fetch <remote branch> && arc reset --hard <remote branch>` &mdash; сбросить рабочую копию до состояния ветки `<remote branch>`, **с потерей локальных изменений**.

После изменений рабочей копии необходимо обновить бету:
```
direct-mk beta-postupdate
```

### Удаление arc-беты

```
direct-delete-beta /var/www/beta.yourlogin.12345
```

При удалении может возникнуть ошибка `The following processes are accessing the working copy`. Это значит, что не все процессы, использующие бету, были остановлены. В таким случае рабочая копия arc не может быть удалена. Необходимо остановить перечисленные процессы, и затем попробовать удалить бету еще раз.

## Разработка perl на бете

После изменения perl кода на бете, необходимо перезапустить apache, чтобы изменения были применены:
```
direct-mk apache-restart
```

Чтобы apache перезапускался автоматически при изменении кода, можно воспользоваться скриптом `./bin/apache_reloader.pl`. После запуска скрипта, при обнаружении изменений файлов в директории беты, apache будет перезапущен. Также, скрипт выводит на экран содеримое `error.log`, позволяя видеть ошибки сборки, либо дебаг-вывод.

## Java-сервисы на бетах

Запущенные на бете java-сервисы будут использоваться для обработки запросов на эту бету.

### Создание беты с java-сервисами

Создать svn-бету с приложением `java-api5`, собранным с патчем из ревью XXXX:
```
direct-create-beta --java app:api5,rp:XXXX
```

Создать аналогичную arc-бету.
```
direct-create-beta --arc --java app:api5,rp:XXXX
```

{% note info %}

По умолчанию, при создании бет с `java-web` из ревью, вместо чекаута и сборки используется приложение собранное в Sandbox. При желании (например, при работе с arc, в котором преимущество сборки в sandbox не так велико), можно использовать флаг `no-sandbox`.  Подробнее: <https://clubs.at.yandex-team.ru/direct-dev/707>

Для `direct-create-beta`:
```
direct-create-beta --java app:web,rp:XXXX,no-sandbox:1
```

Или `java-init`:
```
direct-mk java-init -- --app web --rp XXXX --no-sandbox
```

{% endnote %}

### Запуск java-сервисов на существующей бете

```
direct-mk java-init -- --app api5 --app web --rp XXXX
```

### Обновление java-сервисов

Для обновления java-сервисов (без перла) в svn-бете до текущеге транка или актуального состояния выбранного бранча:
```
direct-mk java-up
```

Применить патч к java-сервисам:
```
direct-mk java-patch -- https://a.yandex-team.ru/review/123456

# Использовать неопубликованную итерацию ревью
direct-mk java-patch -- --draft https://a.yandex-team.ru/review/123456

# Применить патч к определенной ревизии
direct-mk java-patch -- --revision 12345 https://a.yandex-team.ru/review/123456
```

### Пересобрать и перезапустить java-сервисы

```
# Пересобрать все java-сервисы
direct-mk java-ya-make
# Остановить все java-сервисы
direct-mk java-stop
# Запустить все java-сервисы
direct-mk java-start
```

Также, останавливать и запускать java-сервисы можно по отдельности. Настройки nginx при этом не изменяются, запросы все еще будут приходить в остановленные сервисы:
```
direct-mk logviewer-stop 
direct-mk logviewer-start 

direct-mk api5-stop 
direct-mk api5-start

direct-mk intapi-stop 
direct-mk intapi-start

direct-mk web-stop 
direct-mk web-start
```

### Запуск jobs, ess на бетах

Запустить джобу `HotPhrasesSynchronizer` с аргументами `--shard 3`:
```
direct-mk run_java_job HotPhrasesSynchronizer -- --shard 3
```

Логи, аналогично другим java-сервисам, будут в директории `./java/direct/jobs/logs/`

Запуск `full-ess-chain` на бете: [README.md](https://a.yandex-team.ru/arcadia/direct/apps/event-sourcing-system/full-ess-chain/README.md)

### Удаление java-сервисов

```
direct-mk java-cleanup
```

### Изменение уровня логирования java-сервисов { #debug-logs }

По умолчанию для log4j установлен уровень логирования info. Иногда нужны более подробные сообщения (debug, trace). Можно изменить уровень логирования на бете следующим образом:
```
$ ps aux | grep java | grep 10386
alex-ku+ 1039494  0.3  0.5 11712396 1529360 ?    Sl   Mar11  36:19 /usr/local/yandex-direct-jdk11/bin/java ... ru.yandex.direct.intapi.IntapiApp --log-configs-directory /var/www/beta.alex-kulakov.10386/arcadia/direct/libs-internal/config/src/main/resources/
```

У этой беты файлы конфигурации log4j2 находятся в директории `/var/www/beta.alex-kulakov.10386/arcadia/direct/libs-internal/config/src/main/resources/`. Уровни логгирования можно изменять в файле `log4j2-common-loggers.xml`.

После редактирования файла нужно либо перезапустить приложение, либо обновить дату изменения "корневого" файла конфигурации:
```
touch /var/www/beta.alex-kulakov.10386/arcadia/direct/libs-internal/config/src/main/resources/log4j2-production.xml
```

 
## Логи на бетах { #logs }

Логов с беты 8998 нет в логвьювере, нужно подключится на сам сервер `ssh -A 8998.beta1.intapi.direct.yandex.ru` и искать логи там.

Если бета собрана с приложением (например api5), то логи тоже будут не в логвьювере, а на бете.

- `./protected/logs/dbtools_queries.log` — логи запросов к бд из perl
- `./java/direct/api5/logs/` — логи api5, если бета собрана с приложением
- `/var/log/yandex/beta_*_8999/` — логи запросов в баланс, запросов в перловое API, запуска скриптов через ручку и некоторые другие; `*` — логин или бранч автобеты, `8999` — порт беты
- `/var/log/yandex/direct-production/` — некоторые логи могут быть тут
