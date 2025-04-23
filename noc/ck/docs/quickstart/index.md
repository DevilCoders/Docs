# Назначение (draft)
Центральная катка (noc-ck) - это сервис, который призван автоматизировать однотипные операции ("работы") в ходе эксплуатации устройств сетевой инфраструктуры Яндекс.

## Цели и задачи сервиса
- Формализовать и описать сценарии типовых работ на сетевом оборудовании.
    - Нормализация, определение и подготовка настроечных команд с учётом диверсификации производителей оборудования и эксплуатируемого ПО;
    - Переиспользование готовых сценариев;
    - Создание новых сценариев без необходимости непосредственного участия команды NOCDEV;
- Организовать точку входа для выполнения сценариев работ, исключая необходимость ручного управления оборудованием.
- Предоставить высокоуровневый интерфейс для интеграции с действующими сервисами автоматизации NOC, призванными управлять состояниями и настроечными параметрами сетевого оборудования. Такими как:
    - [Racktables](https://racktables.yandex-team.ru), [RTAPI](https://a.yandex-team.ru/arc/trunk/arcadia/noc/rtapi)
    - [Annushka](https://noc-gitlab.yandex-team.ru/nocdev/annushka)
    - [Чекист](https://a.yandex-team.ru/arc/trunk/arcadia/noc/checkist)
    - [Трекер/NOCRFCS](https://st.yandex-team.ru)
- Предоставить интерфейс для интеграции с сервисами автоматизации инфраструктуры Яндекс за пределами NOC (в т.ч. [Wall-E](https://wiki.yandex-team.ru/wall-e/))

# Использование CLI
```bash
# На noc-sas развернут noc-ck-cli
azryve@azryve-osx checkist % ssh noc-sas

# Получаем токен для аутентификации через cli
[azryve@noc-sas ~]$ noc-ck-cli auth
Opening https://oauth.yandex-team.ru/authorize?response_type=code&client_id=155aef63a6d34a57a8c12c4331a66c0b
Please enter the code from the page opened in your browser
OAuth Code: 5067197
OAuth token successfully saved

# Создадим простецтий сценарий который удаляет тег с устройства
[azryve@noc-sas ~]$ cat delete_offline_tag.yml
name: delete-offline-tags
actions:
- name: delete offline tag
  racktables_tag:
    state: absent
    name: в оффлайне
  [azryve@noc-sas ~]$ noc-ck-cli create-declarative < delete_offline_tag.yml
  Declarative scenario saved, kind: delete-offline-tags

# Создадим джобу нового сценария для свитча lab-vla-1s2
# --kind - имя созданного сценария
# --run - сразу запустить джобу
# --no-walle - не уводить нагрузку с тора через walle
[azryve@noc-sas ~]$ noc-ck-cli launch-create --kind delete-offline-tags --run --no-walle lab-vla-1s1
+------------------+--------------------------+
|      Field       |          Value           |
+------------------+--------------------------+
|        id        | 62d807ba728337974db1642f |
|      state       |         running          |
|       kind       |        declarative       |
| declarative_name |   delete-offline-tags    |
|      ticket      |                          |
|     creator      |          azryve          |
|     job_ids      | 62d807ba728337974db16431 |
+------------------+--------------------------+

# После этого за состоянием джобы можно наблюдать по id
# state - planned означает что она готова к запуску
# и начнет выполняться при первой возможности
[azryve@noc-sas ~]$ noc-ck-cli job-show 62d807ba728337974db16431
+----------+--------------------------+
|  Field   |          Value           |
+----------+--------------------------+
|    id    | 62d807ba728337974db16431 |
| hostname |       lab-vla-1s1        |
|  state   |         planned          |
|   kind   |   delete-offline-tags    |
|  ticket  |                          |
+----------+--------------------------+

# В конце она должна будет перейти в state finished
[azryve@noc-sas ~]$ noc-ck-cli job-action-list --format json 62d807ba728337974db16431 | jq '.|.[0]|.state'
"finished"
```


# HTTP API
[Сгенерированная документация swagger](https://ck-test.yandex-team.ru/api/#/)



# Деплой и конфигурация

Конфигурация находится в Аркадии:

* [admins/salt-media/.../noc-ck/config.yml-production](https://a.yandex-team.ru/arcadia/admins/salt-media/noc/roots/units/nocdev-ck/files/etc/noc-ck/config.yml-production)
* [admins/salt-media/.../noc-ck/config.yml-testing](https://a.yandex-team.ru/arcadia/admins/salt-media/noc/roots/units/nocdev-ck/files/etc/noc-ck/config.yml-testing)
* [admins/salt-media/.../nocdev-4k/etc/](https://a.yandex-team.ru/arcadia/admins/salt-media/noc/roots/files/nocdev-4k/etc)

Если хочется что-то поправить, надо оформить пуллреквест на эти файлы в [команду сетевой автоматизации](https://staff.yandex-team.ru/departments/yandex_mnt_noc_dev_dep55049), которую потом и попросить раскатить.

Правки CKron именно в этих конфигах и производятся.

Физически инстансы ЦК и ЧК расположены в [LXC-контейнерах `{гипервизор NOCDEV}`](https://racktables.yandex-team.ru/index.php?page=depot&tab=default&cft[]=1900)

