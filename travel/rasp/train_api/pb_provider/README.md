## pb_provider
Провайдер протобаф ресурсов, создаваемых из админки поездов.

### Новые репозитории протобаф ресурсов
Новые репозитории создаются в [этой папке](https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/python/dicts/trains)
на основе базового [класса](https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/python/dicts/base_repository.py).

### Загрузка данных
В файле `data_provider.py` необходимо создать новый репозиторий и указать файл, из которого будут загружаться данные.
Обычно, это также значит, необходимость добавить ресурс компонентам в qloud для [train-api](https://platform.yandex-team.ru/projects/rasp/train-api/).
Как это сделать написано [здесь](https://st.yandex-team.ru/TRAINS-5366#5e790ff50b67f4308ae669bc).
