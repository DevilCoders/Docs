[[toc]]

# Summary
Инфоточки используют mongodb как основную базу для хранения дорожных событий, информации о пользователях, черного списка фраз, а так же для хранения локов операций (то есть БД используется в качестве сервиса координации инстансов инфоточек).<br>
В качестве драйвера для подключения используется mongocxx.<br>
MongoDB развернута в Yandex.Cloud в конфигурации `replica set` из 3х инстансов в разных ДЦ с `read preference` равным `primary`, `read concern` равным `local` и `write preference` равным `1` во всех операциях. Из этого следует:
1. чтение и запись всегда происходят из/в primary инстанса монги;
2. как следствие пункта 1, увеличение числа инстансов не увеличивает производительность БД, а только влияет на отказоустойчивость;
3. в случае отказа одного ДЦ возможна потеря данных даже после их успешного чтения до момента отказа, ну то есть пользователь успешно поставил и прочитал точку, а после отказа primary инстанса и восстановления реплики этой точки уже не будет в базе (почему так см. `read concern` и `write concern` в документации монги);
4. с поправкой на пункт 3, база данных переживает -1 ДЦ.

# Instances
Облако: `maps-core-jams-infopoints`<br>
Каталог: [`maps-core-jams-infopoints`](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7)<br>
| Environment | Cluster Name |
|---|---|
| stable | [maps-core-jams-infopoints-stable](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb/cluster/mdb4j4tmaggqne1co4k2) |
| testing | [maps-core-jams-infopoints-testing](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb/cluster/mdbsjmc9n0bhp67tlm0q) |
| load | [maps-core-jams-infopoints-load](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb/cluster/mdbgkkn2d755p51mmuot) |

# Monitorings
## Web UI
За состоянием состояния реплики можно наблюдать в [web ui](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb) во вкладках `Мониторинг` и `Хосты`.
## Juggler
| Environment | URL |
|---|---|
| stable | [maps_core_jams_infopoints_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_stable%26service%3D*-mdb-*) |
| testing | [maps_core_jams_infopoints_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_testing%26service%3D*-mdb-*) |
| load | [maps_core_jams_infopoints_load](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_load%26service%3D*-mdb-*) |

# How to deploy
Проще всего накликать через [web ui](https://yc.yandex-team.ru/cloud). У сервиса уже должно быть свое облако (в выпадающем списке облаков выбрать `maps-core-jams-infopoints`).
1. На вкладке облака, если в нем еще нет каталога `maps-core-jams-infopoints`, то создать его (через `Создать каталог`).
1. Перейти в каталог -> `Managed service for MongoDB`.
1. Нажать `Создать кластер`, выбрать окружение `Production` (даже для testing и load), версия `4.0` (такая версия поддерживается драйвером на момент написания документа), имя БД `points`, имя пользователя `infopoints`, пароль придумай сам, добавить хосты в нужных ДЦ (man, vla, sas). Имя пользователя и пароль нужно положить [в секретницу](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint?rev=6746288#secrets). Класса хоста 4 Cores/16ГБ должно быть достаточно для ~1000 rps.
1. Перейти в каталог `Базы данных` вновь созданного кластера, создать еще одну базу с именем `event_log`.
1. Перейти в каталог `Пользователи` вновь созданного кластера, выдать пользователю `infopoints` права `readWrite` на базу данных `event_log`.
1. [Выполнить](#how-to-connect) на вновь созданном кластере [скрипт для создания индексов для базы points](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/database/create_points_indexes.js).
1. [Выполнить](#how-to-connect) на вновь созданном кластере [скрипт для создания индексов для базы event_log](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/database/create_event_log_indexes.js).
1. Указать новые fqdn хостов в [`maps/infopoint/conf/database.json.(stable|testing|load)`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/conf).
1. В няне добавить/переключить в `Environment variables configuration` переменные окружения `INFOPOINTS_DB_USERNAME` и `INFOPOINTS_DB_PASSWORD` на новые версии секретов. 

# How to connect
Для подключения требуется mongo-shell версии 4.0. Возможно подключение и без ssl, тогда из комманды нужно убрать опции `--ssl` и `--sslCAFile`. Значение `{{database}}` подставлять `points` или `event_log`, в зависимости от целевой базы данных. Значение `{{password}}` брать из секретницы.<br>
Команду для подключения можно найти на [странице](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb?section=list), выбрав нужное окружение и нажав кнопку "Подключиться".

# How to manage
Управлять репликой можно через [web ui](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb) или CLI ([документация](https://doc.yandex-team.ru/cloud/cli/index.html)).

# What can go wrong
На данный момент по результатам стрельб узким местом является ширина канала сети, для увеличения нужно изменить класс хоста (например, s2.small -> s2.medium). Менять класс хоста можно без даунтайма и переезда, изменив настройки кластера в [web ui](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb) (`Обзор` -> `Изменить кластер`) или через [CLI](https://doc.yandex-team.ru/cloud/cli/index.html).<br>
На случай потери данных mdb ежевдневно в 22:00 делает [бэкапы](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb?section=backups).

## How to restore backup
Резервные копии создаются автоматически в mdb каждые сутки ближе к полуночи.<br>
Чтобы восстановить резервную копию mdb через web ui, нужно [тут](https://yc.yandex-team.ru/folders/foonovv3vhln4oqqn8e7/managed-mongodb) выбрать нужный кластер, перейти на страницу `Резервные копии` и напротив нужной копии нажать `Восстановить кластер`.<br>
Резервная копия в mdb восстанавливается в новый кластер. Необходимо иметь достаточную свободную квоту для создания этого кластера, желательно иметь эту квоту про запас на случай восстановления, в крайнем случае можно уменьшить размер инстансов в testing/load окружениях, чтобы освободить квоту. На момент написания документа, при создании кластера размер диска должен быть не меньше размера исходного кластера на момент создания копии: если кластер А имеет размер диска 30ГБ на инстанс на момент создания копии, а после создания размер диска уменьшили до 15ГБ, то при восстановлении размер диска создаваемого из копии кластера должен быть не меньше 30ГБ (нужное минимальное значение размера диска выставляется по умолчанию само в поле ввода размера диска нового кластера). Число ядер/RAM в создаваемом кластере можно задавать любым, по умолчанию в полях указания числа ядер/RAM выставляются параметры исходного кластера (вместо которого мы создаем новый из резервной копии), но лучше перепроверять. При создании нового кластера стоит не забыть добавить хосты в разных ДЦ (если необходимо). Имя базы данных, имя пользователя и пароль для подключения восстанавливаются из копии.<br>
Свободную квоту по mdb можно смотреть [здесь](https://dispenser.yandex-team.ru/db/projects/maps-core-jams-infopoints).
Так как при восстановлении копии создается новый кластер, имена хостов созданной реплики будут отличаться от имен хостов исходного кластера. Чтобы подключиться к новуму кластеру, стоит поменять нужный `database.conf` [тут](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/conf) и не забыть перезагрузить infopoint (`yacare restart infopoint`) если изменения в конфиге делаются на самих хоста infopoints, а не через раскатку нового образа. Если критично, чтобы все хосты infopoints подключились одновременно к новому кластеру, то нужно на всех хостах отредактировать `database.conf`, потом на всех хостах остановить infopoints (`yacare stop infopoint`), потом на всех хостах запустить infopoints (`yacare start infopoint`). В противном случае, если перезагружать infopoints по очереди через `yacare restart infopoint` или обновлять конфиг через раскатку нового образа, то в течении какого-то времени разные инстансы infopoints будут смотреть в разные кластеры mdb (исходный и созданный из копии), что, в общем-то, не критично (будет повышенный уровень 404), если при этом невалидные данные в исходном кластере не будут портить данные в новом кластере, например, через запросы пользователей или другие неявные связи.

# Secrets
Пароли хранятся [в секретнице](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint?rev=6746288#secrets)
