### Yandex Cloud Clusters

#### Описание
В словаре `yc_clusters` находятся данные о кластерах, полученные из API Yandex Cloud (https://yc.yandex-team.ru)

{% cut "Пример словаря" %}
```python
yc_clusters = {
    "mdb7lttvnv3vomtq2f0s": {
        "type": "postgresql",
        "version": "12",
        "name": "airflow_postgresql",
        "hosts": [
            {
                "fqdn": "man-n94orrvcxn38tsxt.db.yandex.net",
                "dc": "man",
                "shard": "noshard"
            },
            {
                "fqdn": "sas-lmrjzxby9ry9et3e.db.yandex.net",
                "dc": "sas",
                "shard": "noshard"
            }
        ],
        "folder_id": "foori5uktoh2v12cbltq",
        "description": "postresql для airflow аналитиков",
        "id": "mdb7lttvnv3vomtq2f0s"
    },
    "mdbr7mc969bedk48vhl1": {
        "description": "Монга для Базинги. Продакшен.",
        "id": "mdbr7mc969bedk48vhl1",
        "folder_id": "foori5uktoh2v12cbltq",
        "hosts": [
            {
                "shard": "rs01",
                "dc": "man",
                "fqdn": "man-5lhxezsk0cui0kdf.db.yandex.net"
            },
            {
                "fqdn": "sas-9exbl0ftdyxaih26.db.yandex.net",
                "dc": "sas",
                "shard": "rs01"
            },
            {
                "fqdn": "vla-mslk73b98idch9wv.db.yandex.net",
                "dc": "vla",
                "shard": "rs01"
            }
        ],
        "type": "mongodb",
        "version": "4.2",
        "name": "bazinga-prod"
    },
},
```
{% endcut %}

#### Переодичность обновления
На момент написания составляет 10 минут. Уточнить значение можно в [конфиге](https://bishop.mtrs.yandex-team.ru/program/bishop-helper/config/metrika.deploy.infra.bishop.helper.production/active) bishop-helper-а

#### Получение данных
Для получения данных robot-metrika-bishop должен иметь доступ к облачной консоли. Для этого ему должна быть выдана роль "Пользователь MDB" в соответствующем ABC-сервисе.
Какие облака/каталоги будет забирать к себе bishop, задаётся в конфиге bishop.
