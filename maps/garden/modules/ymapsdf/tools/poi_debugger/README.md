# poi_debugger

В модуле `ymapsdf` происходит объединение данных НЯК и Справочника.
Это процесс сложен и запутан. Подробности [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/README.md#merge_poi).

Тул `poi_debugger` позволяет анализировать, почему в финальные таблицы `ymapsdf` попали те или иные данные.

Пример запуска:
```
/poi_debugger --ft-id=4325275488 --shipping-date=20211223_702165_2510_242688804 --region=cis1
```
