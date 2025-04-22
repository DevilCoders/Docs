# Вертикальный Tableau
[https://tableau.vertis.yandex.net](https://tableau.vertis.yandex.net/)

## Где живёт
Группа для наших Windows-серверов под крылом [Win-админов](#kontakty): [%vertis_win](https://c.yandex-team.ru/groups/vertis_win)
### Прод
#### Физические сервера:

[win-02-sas.prod.vertis.yandex.net](https://bot.yandex-team.ru/umka/assets/900904969)
[win-02-myt.prod.vertis.yandex.net](https://bot.yandex-team.ru/umka/assets/900158204)

#### Адреса виртуальной машины (ВМ одна, но имеет разные адреса в зависимости от ДЦ, в котором запущена):

```tableau-ha-myt.ld.yandex-team.ru```
```tableau-ha-sas.ld.yandex-team.ru```

### Тестинг
#### Физический сервер:

[win-01-sas.prod.vertis.yandex.net](https://bot.yandex-team.ru/umka/assets/900156482)

Виртуальная машина:

```tableau-win-sas.vertis.yandex.net.```

Ко всем вышеуказанным ВМ в тестинге и проде можно подключиться по RDP, доступ в случае необходимости просить у [Win-админов](#kontakty).

## Особенности
Используем Windows-версию Tableau Server. Номер версии на момент написания доки: 2021-2-0.

Используется доменная аутентификация пользователей.

Физические сервера закреплены за Вертикалями, но Windows на них, а так же виртуальные машины, Windows внутри ВМ, репликация - всё это находится в ведении Windows-админов, и вопросы решаются через них (см. [Контакты](#kontakty)).

### Репликация
В проде сервис живёт в виртуальной машине в единственном экземпляре, реплицируется через Hyper-V Replication: в каждый момент времени ВМ запущена на одном из двух физических серверов, при этом все изменения на виртуальном жёстком диске постоянно реплицируются на второй физический сервер. При необходимости - запланированной или аварийной недоступности физического сервера, на котором в данный момент выполнялась ВМ, силами Windows-админов ВМ "переключается" на противоположный сервер: ВМ останавливается на текущем сервере, дожидаемся пока все изменения на диске дореплицируются на второй сервер, после чего ВМ запускается на втором сервере. При этом репликация дисковых изменений продолжает работать (при доступности обоих физических серверов), но уже в противоположную сторону.

В тестинге сервис так же живёт в ВМ, но без репликации. Хост-машина одна, отказоустойчивости нет.

### Веб-балансировщик
Не совсем балансировка, т.к. активный сервер всегда только один.
Точка входа - кластер nginx [%vertis_vprod_lb_int_nginx](https://c.yandex-team.ru/groups/vertis_vprod_lb_int_nginx), конфигурация описана в пакете [yandex-vertis-config-nginx-front-internal](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front-internal).
В качестве апстрима указан cname `tableau-ha.vertis.yandex.net`, через цепочку cname указывающий на текущий адрес ВМ с Tableau. Пример в случае, когда сервис выполняется в ДЦ MYT:
```
➜  ~ host tableau-ha.vertis.yandex.net
tableau-ha.vertis.yandex.net is an alias for tableau-ha.ld.yandex-team.ru.
tableau-ha.ld.yandex-team.ru is an alias for tableau-ha-myt.ld.yandex-team.ru.
tableau-ha-myt.ld.yandex-team.ru has IPv6 address 2a02:6b8:c03:7be:8000:40ab:3216:66eb
```
При переключении в другой ДЦ cname домена `tableau-ha.ld.yandex-team.ru` переключается на соответствующий адрес ВМ (см. [Переключение в другой ДЦ](#pereklyuchenie-v-drugoj-dc)), а в конфигурации nginx указан укороченный DNS TTL в 10 секунд. nginx подхватывает изменения в DNS и начинает форвардить запросы по новому адресу.

Для тестинга балансировщик не предусмотрен. Ходить в сервис можно либо по адресу ВМ, либо локально изнутри ВМ, подключившись к ней по RDP.

## Переключение в другой ДЦ
Переключение Tableau в другой ДЦ (например, перед учениями) производится по согласованию с [Win-админами](#kontakty), процесс можно описать следующими шагами:

  - логинимся по RDP на виртуалку, доступную по одному из адресов в зависимости от того, в каком ДЦ она сейчас запущена
  - на всякий случай смотрим статус сервиса, для этого в браузере логинимся в Tableau Services Manager (TSM) по адресу: [https://localhost:8850/#/status](https://localhost:8850/#/status)
    Логинимся своей доменной учётной записью, либо пользователем [robot-vertisbi-admin](#kredy-licenzii)
    Если все пункты зелёные в состоянии Active - значит всё ок
  - Останавливаем Tableau одним из двух способов:
    - через веб-консоль TSM: в правом верхнем углу видим контрол "Tableau Server is running", и выбираем там "Stop Tableau Server"
    - через обычную cmd-консоль выполняем:
    ```
    tsm stop
    ```
  - дожидаемся, пока завершится процесс остановки Tableau (обычно это несколько минут)
  - разлогиниваемся с ВМ и сообщаем Windows-админам, что можно выполнять её переключение
  - Windows-админы останавливают ВМ в текущем месте, дожидаются окончания репликации, после чего запускают ВМ на сервере в другом ДЦ (см. [репликация](#replikaciya)).
    Кроме того, Windows-админы переключают в DNS cname `tableau-ha.ld.yandex-team.ru` на адрес, содержащий AAAA-запись соответствующей ВМ, которая становится активной.
    Пример в случае, когда Tableau выполняется в ДЦ MYT:
    ```
    ➜  ~ host tableau-ha.ld.yandex-team.ru
    tableau-ha.ld.yandex-team.ru is an alias for tableau-ha-myt.ld.yandex-team.ru.
    tableau-ha-myt.ld.yandex-team.ru has IPv6 address 2a02:6b8:c03:7be:8000:40ab:3216:66eb
    ```
  - После того, как ВМ становится доступной по новому адресу, логинимся на неё по RDP
  - дожидаемся, пока запустятся вспомогательные сервисы Tableau. Проконтролировать это можно через консоль управления сервисами:
    `Win+r`, выполняем команду `services.msc`. В консоли находим сервисы, начинающиеся на слово "Tableau" и дожидаемся, пока они все перейдут в состояние "Running". Обновлять их состояние в консоли можно через `Action` > `Refresh`.
    Можно не контролировать, а просто подождать пока станет доступна веб-консоль TSM.
  - запускаем основные компоненты Tableau одним из двух способов: через веб-консоль TSM - аналогично тому, как останавливали (см. выше), либо выполняем в обычной cmd-консоли команду:
    ```
    tsm start
    ```
    Запуск обычно занимает пару десятков минут.
  - дожидаемся, пока запустятся все сервисы. Контролировать процесс можно в TSM-консоли. Смотрим, чтобы в процессе запуска не возникло никаких ошибок.
  - Готово

## Метрики, мониторинги
Дашборд: [Tableau Win](https://grafana.vertis.yandex-team.ru/d/000000014/tableau-win?orgId=1&refresh=10s)

Метрики экспортируются стандартным windows-exporter'ом, и далее скрейпятся из prometheus/VictoriaMetrics. Серверы Tableau для скрейпа описаны статически в [конфигурационном файле](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config/production/scrape.yml) (искать по слову `tableau`).
Помимо системных метрик ОС, экспортер так же умеет экспортировать кастомные метрики из текстовых файлов, для этого их нужно складывать в директорию
```
C:\Program Files\windows_exporter\textfile_inputs
```
Данная фича использована для экспорта состояния бэкапов, см. [Бэкапы](#bekapy).

На основе метрик так же настроены [алерты через VM/Juggler](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config/production/alerts/tableau.rules.yml), сейчас их 2:
  - Tableau_TooFewInstances
  - Tableau_BackupFail

Названия говорят за себя сами.

#### Установка windows-exporter
  - скачиваем последнюю версию с [github-страницы релизов](https://github.com/prometheus-community/windows_exporter/releases) (работоспособность протестирована на версии 0.16.0), качаем файл `windows_exporter-<version>-amd64.msi`
  - устанавливаем
  - готово.

## Бэкапы
Хранятся в S3, бакет `vertis-backups`, директория `/prod/tableau/`.
Выполняются раз в сутки в 02:00 приложением [tableau-backup](https://a.yandex-team.ru/arc_vcs/classifieds/infra/tableau-backup).
Инициируются через Windows scheduler.
Процесс состоит из следующих шагов:
  - инициируется создание стандартного бэкапа средствами Tableau, для этого [запускается команда](https://a.yandex-team.ru/arc_vcs/classifieds/infra/tableau-backup/main.go?rev=r9367440#L81):
    ```
    tsm maintenance backup -u <robot_username> -f <filename> -k
    ```
  - дожидаемся пока завершится процесс формирования бэкап-файла
  - заливаем в S3
  - удаляем локальный файл бэкапа

Ведётся лог-файл последнего выполнения бэкапа, файл `backup.log`, расположен в директории
```
C:\ProgramData\Tableau\Tableau Server\data\tabsvc\files\backups
```

### Настройка бэкапов
Настройку бэкапов после (пере)установки Windows и/или Tableau можно описать следующими шагами:
  - собираем `tableau-backup` из исходников:
    - клонируем репо [https://a.yandex-team.ru/arc_vcs/classifieds/infra/tableau-backup](https://a.yandex-team.ru/arc_vcs/classifieds/infra/tableau-backup?rev=r9367440)
    - собираем:
    ```
    go get github.com/konsorten/go-windows-terminal-sequences
    bash build.sh
    ```

  - получившийся бинарник кладём на Windows-хост с Tableau в директорию:
    ```
    C:\ProgramData\Tableau\Tableau Server\data\tabsvc\files\backups
    ```

  - туда же кладём файл [`backup.ps1`](https://a.yandex-team.ru/arc_vcs/classifieds/infra/tableau-backup/backup.ps1?rev=r9367440)

  - Скачиваем и устанавливаем AWS CLI `AWSCLI64.msi` со страницы [https://aws.amazon.com/ru/cli/](https://aws.amazon.com/ru/cli/)

  - Проверяем существование директории:
    ```
    C:\Program Files\windows_exporter\textfile_inputs
    ```
    Директория должна была создаться в процессе установки windows-exporter'а (см. [Метрики, мониторинги](#metriki-monitoringi)). В неё скрипт бэкапа будет складывать файл со статусом выполнения, который затем будет экспортирован в виде метрики.

  - Настраиваем задачу в стандартном Windows-шедулере:

    - Скачиваем готовый файл с описанием задания для Windows Scheduler [здесь](https://a.yandex-team.ru/arc_vcs/classifieds/infra/tableau-backup/Tableau%20backup.xml?rev=r9367440)
    - в Панели управления Windows через поиск находим и открываем `Schedule tasks`, открывается `Task Scheduler`
    - выбираем в дереве `Task Scheduler Library`, нажимаем `Action` > `Import Task...`, выбираем скаченный файл описания задания для Windows Scheduler. Проверяем, что в поле `When running the task, use the following user account:` введён роботный пользователь `robot-vertisbi-admin`. Если нет, то жмём `Change User or Group...`, находим пользователя в `Entire Directory` и используем его
    - При сохранении спрашивает пароль от пользователя `robot-vertisbi-admin` - вводим (см. [Креды](#robot-vertisbi-admin))

  Видим наше новое задание в списке.


Здесь сразу же можем проверить работоспособность создания бэкапа. Выделяем задание, `Action` > `Run`, и контролируем выполнение через лог-файл. В конце проверяем наличие результирующего файла бэкапа в S3 в директории с текущей датой.

### Восстановление из бэкапа
Если понадобилось восстановить бэкап, то выполняем следующие шаги.
  - смотрим в S3 список имеющихся бэкапов. Скачиваем на ВМ с Tableau нужный бэкап. Ссылка будет примерно такой:
    ```
    https://s3.mds.yandex.net/vertis-backups/prod/tableau/2021-07-28/tsbackup_data-tableau-ha-2021-07-28.tsbak
    ```
  - пока скачивается бэкап останавливаем Tableau - через веб-TSM, или в cmd-консоли:
    ```
    tsm stop
    ```
  - Скаченный файл бэкапа перекладываем в директорию:
    ```
    C:\ProgramData\Tableau\Tableau Server\data\tabsvc\files\backups\
    ```
  - запускаем импорт бэкапа командой в cmd-консоли:
    ```
    tsm maintenance restore --file <file_name>
    ```
    Пример:
    ```
    tsm maintenance restore --file tsbackup_data-tableau-ha-2021-07-28.tsbak
    ```
  - ждём окончания, контролируя процесс в cmd-консоли, и/или в веб-TSM, куда будет транслироваться текущий прогресс. Импорт займёт несколько десятков минут
  - после окончания процесса импорта бэкапа запускаем Tableau через веб-TSM или через cmd-консоль:
    ```
    tsm start
    ```
  - не забываем удалить файл, из которого восстановили бэкап


## (пере)наливка
Все операции с железными серверами, с ВМ, с ОС выполняются через [Windows-админов](#kontakty).

### Windows
  - имя компьютера (Full computer name):
  ```
  tableau-ha.ld.yandex-team.ru
  ```
  - для того, чтобы были доступны ресурсы из внешнего Интернета, в качестве DNS-сервера нужно указать адрес фермы nat64:
  ```
  2a02:6b8:0:3400::5005
  ```
  Остальные DNS-адреса нужно удалить. Windows-админов нужно попросить отключить смену адреса DNS в свойствах ВМ, чтобы эта настройка не перетиралась при перезагрузке.
  - у ВМ нужно совсем отключить протокол ipv4. Для этого в свойствах виртуального сетевого адаптера, в разделе "This connection uses the following items:" нужно снять галку напротив пункта "`Internet Protocol Version 4 (TCP/IPv4)`"
  - Так же нужно попросить Windows-админов сделать следующие настройки ВМ статическими, чтобы они не изменялись при переключении ВМ в другой ДЦ:

    - MAC address
    - Virtual Machine ID

### Tableau
#### ATR
В самом начале установки Tableau нужно выбрать способ активации лицензии `Use ATR for product activation`. Опция нужна для того, чтобы лицензия не слетала при переключении Tableau в другой ДЦ (см. [Креды, лицензии](#kredy-licenzii)). В случае, если в инсталляторе данная опция окажется недоступна, нужно в редакторе реестра (`Win+r` > `regedit`) найти и удалить ключ:
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Tableau\ATR]
```
После перезапуска инсталлятора опция должна стать активной. Расследовали хак здесь: [VERTISADMIN-26405](https://st.yandex-team.ru/VERTISADMIN-26405#60e84c8a33792e40f9ccaf17)

После установки Tableau нужно уменьшить интервал переактивации ATR до минимума, делается это через cmd-консоль:
```
tsm licenses atr-configuration set -–duration 14400
tsm pending-changes apply
net stop tabadmincontroller_0
net start tabadmincontroller_0
```

#### Identity store
После установки, во время инициализации Tableau в качестве Identity Store выбираем "Active Directory". Все поля оставляем как есть, судя по всему Tableau успешно подтягивает настройки из Windows, которая сама в домене.

#### Administrator account
После завершения процесса инициализации предлагается создать учётную запись администратора:
```
Create a server administrator account to access Tableau Server
```
Здесь логинимся роботным пользователем `robot-vertisbi-admin` (см. [креды](#robot-vertisbi-admin)), наделяя его правами администратора в данной инсталляции Tableau. В последствии, при необходимости, можно будет логиниться этим пользователем в Tableau и выполнять действия, требующие административных привилегий.

#### Переустановка
Если по какой-то причине мы хотим полностью переустановить Tableau (например, что-то идёт не так, и мы не можем это починить), то последовательность действий будет такая:
  - Удаляем Tableau штатным образом: в Панели управления Windows открываем "Apps", там находим "Tableau Server <версия>" и жмём "Uninstall"
  - скачиваем скрипт [tableau-server-obliterate.txt](https://kb.tableau.com/servlet/fileField?retURL=%2Farticles%2Fissue%2Fwindows-server-obliterate-script-is-not-available-after-running-uninstall&entityId=ka40d000000H7glAAC&field=Attachment__Body__s)
    Сохраняем его куда-нибудь в `C:\Utilz\`
    И выполняем в консоли cmd, запущенной от Администратора:
    ```
    C:\Users\wf1nder>cd c:\Utilz
    c:\Utilz>tableau-server-obliterate.cmd -a -y -y -y
    ```
    Немного подробностей про удаление и скрипт: [раз](https://help.tableau.com/current/server/en-us/remove_tableau.htm), [два](https://kb.tableau.com/articles/issue/windows-server-obliterate-script-is-not-available-after-running-uninstall).
  - Перезагружаем Windows
  - Устанавливаем Tableau обычным образом

### clickhouse-odbc
Для того, чтобы была возможность работать с базами ClickHouse, необходимо установить драйвер `clickhouse-odbc`. Для этого качаем и устанавливаем последнюю версию со страницы релизов [отсюда](https://github.com/ClickHouse/clickhouse-odbc/releases).
Нам нужен файл:

```
clickhouse-odbc-<version>-win64.msi
```

После установки драйвера обязательно требуется перезагрузка Windows, несмотря на то, что сам установщик clickhouse-odbc может об этом не попросить.
Перед перезагрузкой лучше остановить Tableau один из двух способов:
    - через веб-консоль TSM: в правом верхнем углу видим контрол "Tableau Server is running", и выбираем там "Stop Tableau Server"
    - через обычную cmd-консоль выполняем:
    ```
    tsm stop
    ```

После перезагрузки, соответственно, нужно запустить Tableau: через веб-консоль TSM - аналогично тому, как останавливали (см. выше), либо выполняем в обычной cmd-консоли команду:
    ```
    tsm start
    ```

Запуск Tableau обычно занимает пару десятков минут.

### Установка windows-exporter
см. [Установка windows-exporter](#ustanovka-windows-exporter)

### Настройка бэкапов
см. [Настройка бэкапов](#nastrojka-bekapov)

## Креды, лицензии
Лицензиями управляет Олег Тараканов, см. [Контакты](#kontakty).
Список лицензионных ключей в секретнице: [yav](https://yav.yandex-team.ru/secret/sec-01er4eeqy16kv8tfc6he07zpvd/explore/versions) (похоже, неактуальный в данный момент).

Для активации Tableau используем Authorization-To-Run (ATR), эта опция включается в инсталляторе Tableau Server на одном из начальных шагов.
Подробнее про ATR [здесь](https://help.tableau.com/current/server/en-us/atr_service.htm).
Некоторые наши изыскания про ATR и слёт лицензий при переключении в другой ДЦ: [VERTISADMIN-26405](https://st.yandex-team.ru/VERTISADMIN-26405#60e84c8a33792e40f9ccaf17)

### robot-vertisbi-admin
Роботный пользователь, используется:
  - в качестве системного Windows-пользователя, от которого запускаются бэкапы, возможно что-то ещё
  - в качестве админ-пользователя в Tableau

Стафф: [robot-vertisbi-admin](https://staff.yandex-team.ru/robot-vertisbi-admin)
Пароль: [yav](https://yav.yandex-team.ru/secret/sec-01d86jwrz57vm0v27f6mpbhj6m/explore/versions)


## Контакты
С нашей стороны всем, что связано с Tableau, ведает [Служба аналитики вертикальных сервисов](https://staff.yandex-team.ru/departments/yandex_personal_vertserv_internal_marketing/), конкретно - [Олег Тараканов](https://staff.yandex-team.ru/olegtar).
Телеграм-чат: [verticals-tableau](https://t.me/joinchat/W4nT_qhHiJ9lZWNi)
Очередь Windows-админов в трекере: [WINADMINREQ](https://st.yandex-team.ru/WINADMINREQ)
