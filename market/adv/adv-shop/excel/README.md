## Библиотека для подключения common-excel

1. ```ru.yandex.market.adv.config.ExcelAutoconfiguration``` - автоконфигурация для сервисов для вычитывания excel файла
   и его дальнейшей обработки.
2. ```ru.yandex.market.adv.service.excel.ExcelMdsFileService``` - сервис для вычитывания excel файла из mds и его
   дальнейшей обработки. Инициализируется как bean с названием ```excelMdsFileService```, если есть
   bean ```ru.yandex.market.adv.client.MdsClient```.
