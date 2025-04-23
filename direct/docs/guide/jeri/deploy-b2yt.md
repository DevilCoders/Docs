# Выкладка релизов b2yt (Репликатор)

**Не путать с Зекрализатором (mysql2yt-full).** Про него читать здесь: <https://wiki.yandex-team.ru/jeri/m2yt-full/>

## Что где { #cluster-structure }

### Кто какую версию данных пишет и в какой кластер
Записано в переменных окружения конкретного стейджа
YT_SYNC_CLUSTER_NAME - имя кластера YT
YT_SYNC_CLUSTER_STATE - стейбл льем или prestable
YT_SYNC_MYSQL_SERVER_ID - server-id для процесса mysql
YT_SYNC_VERSION - версия данных


### Стейджы в deploy
<https://deploy.yandex-team.ru/stages/direct-java-b2yt-man-production> - пишет в seneca-man
<https://deploy.yandex-team.ru/stages/direct-java-b2yt-sas-production> - пишет в seneca-sas
<https://deploy.yandex-team.ru/stages/direct-java-b2yt-vla-production> - пишет в seneca-vla


## Релиз без смены версии данных { #release-simple }

1. Поменять версию через `direct-version-set`
2. Выбрать один кластер YT, например Seneca-Man
3. Выложить на все машины, пишущие текущую версию данных на выбранный кластер. Выложить == пакеты + рестарт сервиса
4. Подождать (обычно хватает получаса, чтобы оценить, что процесс работоспособен и не падает)
5. Выложить на машины, пишущие текущую версию данных на остальные кластеры


## Релиз со сменой версии данных (=с реимпортом) { #release-with-reimport }


### Про порядок { #reimport-order }

На каждом кластере должно случиться, порядок строгий: 

- удаление старых таблиц (=неиспользуемая версия данных, -1 от текущей версии продакшена; текущую версию данных не трогаем)
- генерация новых таблиц
- переключение линка current
- остановка импорта предыдущей версии

Между шагами могут быть паузы.
Между кластерами порядок нестрогий. 

Дополнительные соображения:  
- не растягивать время, когда current указывает на данные разных версий. Сутки &mdash; нормально, неделя &mdash; не очень
- в целом не давать деплою растягиваться слишком надолго

### Про инструменты { #reimport-tools }

Релиз с реимпортом &mdash; долгий и многошаговый процесс.
Для учета что уже сделано, что еще нет, используем скрипт `dt-mysql2yt-release-order`, работает например с ppcdev.
Этот же скрипт подсказывает, как выполнить следующие действия. 

Важно! Сейчас скрипт сам ничего не меняет на контейнерах с приложением и в Сенеках.
Выкладку, запуск/перезапуск, манипуляции с симлинками и каталогами делает человек.
Скрипт работает как чеклист с подсказками. 

### Выкладка релиза с реимпортом { #how-to-deploy }

Для того, чтобы запустить заливку новой версии надо взять стейдж <https://deploy.yandex-team.ru/stages/direct-java-b2yt-prestable> и в нем:
1. Проставить переменные окружения про версию, кластер - <https://deploy.yandex-team.ru/stages/direct-java-b2yt-prestable/config/du-java-b2yt-multi-cluster-set/box-java-b2yt-box/wl-java-b2yt-workload>
2. Добавить подов в нужном ДЦ <https://deploy.yandex-team.ru/stages/direct-java-b2yt-prestable/edit/du-java-b2yt-multi-cluster-set>


Посмотреть список релизов: `dt-mysql2yt-release-order list`

1. Инициализировать чеклист для релиза: `dt-mysql2yt-release-order init-release -t DIRECT-NNNN`
2. Посмотреть состояние релиза: `dt-mysql2yt-release-order -t DIRECT-NNNN` (="таблица с галочками")
3. Заполнить версию кода и данных: `dt-mysql2yt-release-order -t DIRECT-NNNN set-versions --code-version 1.MMMMM.LLLLL-1 --data-version v.Y --prev-data-version v.Z`  
можно заполнять версии по отдельности: `dt-mysql2yt-release-order -t DIRECT-NNNN set-versions --code-version 1.MMMMM.LLLLL-1`  
4. Выбирать действия из подсказок скрипта `dt-mysql2yt-release-order -t DIRECT-NNNN`
5. Что сделано/закончилось &mdash; отмечать командой done, пример: `dt-mysql2yt-release-order -t DIRECT-97323 done -d initial_import_started -c seneca-vla`  
название действия (`-d`) и кластера (`-c`) &mdash; как в таблице с галочками

Время от времени полезно постить в релизный тикет вывод `dt-mysql2yt-release-order -t DIRECT-NNNN`


### Первичный импорт через Transfer Manager { #initial-import-via-tm }

1. Остановить репликатор на ноде-источнике: `sv stop /etc/service/binlog-to-yt-sync`
2. Проверить на YT источнике, что блокировок нет(процесс репликатора остановлен)
3. На ppcback* машинах запустить скрипт `yt-copy-tables`. Примеры:
- Копирование с seneca-man и восстановление(конвертирование в динамические) на seneca-sas: `yt-copy-tables -enable-convert-tables -enable-copy-tables -yt-src-cluster seneca-man -yt-src-directory //home/direct/mysql-sync/v.14 -yt-dst-directory //home/direct/mysql-sync/v.14 -yt-dst-cluster seneca-sas -yt-token /etc/direct-tokens/yt_robot-direct-yt`
- Копирование с seneca-man на seneca-sas без конвертирования: `yt-copy-tables -enable-copy-tables -yt-src-cluster seneca-man -yt-src-directory //home/direct/mysql-sync/v.14 -yt-dst-directory //home/direct/mysql-sync/v.14 -yt-dst-cluster seneca-sas -yt-token /etc/direct-tokens/yt_robot-direct-yt`
- Получить справку по программе с примерами: `yt-copy-tables -h`

{% note info  %}

В процессе копирования с источника, сохраняется информация о ключах в таблетсетах. Эти таблицы называются <table_name>\_pivot и будут удалены после конвертирования static в dynamic. Процесс копирования и конвертирования должен завершиться без ошибок в выводе stdout: сообщения с префиксом ERROR говорят о проблемах при работе. Успешное выполнение копирования завершается фразой `STEP1. success`, конвертирования - `STEP2. success`

{% endnote %}

4. Запустить репликатор на ноде источнике и на ноде приёмнике: `sv start /etc/service/binlog-to-yt-sync`
5. Убедиться в отсутствии ошибок в логах программы: `tail -f /var/log/yandex/messages.log.*`



### Ручное выполнение операций 

{% note info  %}

В норме все команды должен правильно подсказывать `dt-mysql2yt-release-order`.  
Если он этого не делает, стоит исправить скрипт. 

{% endnote %}

TODO перенести полезное со страницы <https://wiki.yandex-team.ru/jeri/java-b2yt-deploy/>


## Ссылки { #links }

- Выкладка Зеркализатора (mysql2yt-full): <https://wiki.yandex-team.ru/jeri/m2yt-full/>
