## Хранение данных договоров
- Основная информация о договоре хранится в MySQL, в `realty_rent`, в таблице `rent_contract`
- PDF-версии договоров сохраняются в Dochub, и так как содержат персональные данные, находятся [в защищенной Palma](https://palma.test.vertis.yandex-team.ru/dictionaries/realty/dochub/documents) c идентификаторами типа `rent.contract.\w+.\d+`

### Настройки генерации 
Для генерации pdf-версии используется версионирование шаблонов в Dochub, для перехода на новую версию необходимо [изменить ее в Palma](https://palma.test.vertis.yandex-team.ru/dictionaries/realty/dochub/renderer/settings).
