Описание задачи
===============

Задача выгружает справочные данные в Sandbox ресурсы.
Задача бинарная, чтобы ее загрузить в локальную песочницу в консоли:
```bash
cd arcadia/sandbox/projects/avia/dump_data/
ya make --checkout
sandbox upload_binary dump_data --enable-taskbox --attr target=avia/sandbox/dump_data
``` 
"target=avia/sandbox/dump_data" - аттрибут по которому сандбокс подхватит новую бинарь

Для заливки в большой sandbox:
```bash
cd arcadia/sandbox/projects/avia/dump_data/
ya make --checkout
./dump_data upload --owner AVIA --attr target=avia/sandbox/dump_data
```

Добавление нового справочника
=============================

- добавляем блок с описанием импорта (arcadia/travel/avia/dump_data/lib/model_declaration.py):
```python
dict(
    country=dict(  # название модели. используется как название (в нижнем регистре) ресурса в sandbox
        model=MysqlModel,
        db_table='www_country',
        proto_model=TCountry,  # proto сериализатор
        fields=[
            dict(proto_attribute='Id', db_column='id'),
            dict(proto_attribute='Title', db_column='title'),
            dict(proto_attribute='GeoId', db_column='_geo_id'),
            dict(proto_attribute='NewLTitleId', db_column='new_L_title_id'),
        ],
    ),
)
```

- добавляем тип ресурса (arcadia/sandbox/projects/Travel/resources/dicts.py):
```python
class TRAVEL_DICT_AVIA_COUNTRY_PROD(TRAVEL_DICT_AVIA_BASE):
    """Справочник стран от Авиа"""
    resource_name = 'country'

```

- добавляем .proto (пример arcadia/travel/proto/dicts/avia/country.proto)
