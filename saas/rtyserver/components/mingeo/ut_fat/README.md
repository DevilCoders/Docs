Запуск без отладчика:
- ya make -tA

Запуск с отладчиком:
- cкачать ресурсы перечисленные в ya.make с сандбокса и положить в директорию с именем, как имя ресурса в ya.make. Для ресурса 10000_russians получится путь 10000_russians/10000_russians.tsv отн. директории запуска
- ya make .
- ya tool gdb --args ./testgeo_ut_fat

