## Механизм Project Id Acl на портах

### Краткое описание

* Пользователи и Walle выставляют в Racktables project_id на порту
* Annushka генерирует конфигурацию acl для ToR-свитчей на основе данных Racktables
* Racktables выкатывает конфигурацию acl на свитчи на которых произошли изменения
* acl настраивается на input от порта к которому подлючен сервер
* acl устроен в виде вайтлиста который пропускает некоторые виды служебного трафика (icmp6, dhcpv6), ipv6 encap, и project_id проассоциированный с портом
* для портов с project_id определенных как "облачные" разрешены project_id на которых не установлен "secured-bit" (см. Рулсет acl)


### Ссылки с подробностями

* Rationale: https://wiki.yandex-team.ru/andrejjabroskin/archive/hbf-security/#nesankcionirovannoeispolzovanieprojectid
* Рулсет acl: https://wiki.yandex-team.ru/azryve/projectid-push/


### Точки входа

#### Данные
* Таблица с маппингами `Yandex_NetProjectsSwPorts`
* Предикат со свитчами на который выкатываются ACL `[project-id acl autodeploy]`
* Определение "облачных project-id" в Annushka `annushka/model/project_id.py`

#### Логика
* Общая логика в Racktables `plugins/ports-project-id.php`
* Логика для UI в Racktables `plugins/js/ports-project-id.js`
* API переключения в Racktables `export/vlanrequest.php`
* Логика генерации конфига в Annushka `annushka/generators/project_id.py`


### Посмотреть конфиг который генерится для свитча

Вся логика лежит в генераторе `project_id`:

```
ann gen -gproject_id <swname>
```


### Дать возможность иметь несколько project_id на порту
Обычно это требуется если у пользователей по каким-то причинам разделен на отдельные макросы тестинг и прод, но запускается он на одном и том же железе. Мы просто добавляем к project_id вешаемому на порт еще несколько project_id, которые будут разрешены на таких портах.

Примеры тикетов:

* [NOCREQUESTS-3743](http://st.yandex-team.ru/NOCREQUESTS-3743)
* [NOCREQUESTS-4925](http://st.yandex-team.ru/NOCREQUESTS-4925)

Для этого нужно

* Поправить в `annushka/model/project_id.py` маппинг `ADDITIONAL_PROJECT_IDS`
* Выкатить [наливочную копию Annushka](../annushka/common)

 
### Дать возможность иметь много разных project_id на порту

Это возможно только пометив project_id который будет вешаться на порт как "облачный". Данная схема предназначена для гипервизоров и обычно связано с тем что проект хочет крутить собственные виртуалки.

Этим способом можно позволить запускать на машине любые project_id, **кроме** тех которые были созданы с опцией *Без возможности поднять в Облаке*.

Примеры тикетов:

* [CSADMIN-20391](http://st.yandex-team.ru/CSADMIN-20391)
* [NOCDEV-942](http://st.yandex-team.ru/NOCDEV-942)
* [NOCDEV-1150](http://st.yandex-team.ru/NOCDEV-1150)

Для этого нужно

* Поправить в `annushka/model/project_id.py` набор `CLOUD_PROJECT_IDS`
* Выкатить [наливочную копию Annushka](../annushka/common)

