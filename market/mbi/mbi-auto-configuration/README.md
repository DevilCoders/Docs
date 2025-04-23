#### pp-common-utils
Утилитные классы для работы с json-файлами, описывающими структуру ПП и группировку в словари.

#### sql-query-builder

Библиотека (JAR) формирования SQL запросов для отчетов/выгрузок с помощью декларативного описания параметров.

Документация по формату файла конфигурации [здесь](https://wiki.yandex-team.ru/MBI/NewDesign/sql-query-builder)


#### Разработка

Создание проекта для IDEA (из аркадийной [директории](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi-auto-configuration)):
```bash
ya ide idea -r ~/IdeaProjects/mbi-auto-configuration-libs -l .
```

Сборка проекта с запуском тестов:
```bash
ya make -A
```

Релиз: [пайплайн в ЦУМ](https://tsum.yandex-team.ru/pipe/projects/mbi/delivery-dashboard/mbi-auto-configuration-libraries-pipeline)
