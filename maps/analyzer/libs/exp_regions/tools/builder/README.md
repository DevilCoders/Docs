Инструмент для создания файлов, описывающих геометрию регионов, в которых проводятся эксперименты. Ожидает в stdin строки с описаниями полигонов в формате WKT, пишет результат в stdout. Пример использования:

```
echo -e 'POLYGON ((0 0, 1 0, 0 1, 0 0))\nPOLYGON ((1 1, 2 1, 2 2, 1 2, 1 1))' | ./builder > rtree.mms
```
