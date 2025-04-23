# saas-java-client - Билиотеки для взаимодействия с SaaS

* **Используется:** MBO (searcher, YT indexer).
* **Состояние:** как прямо библиотека под все-все кейсы не доводилась.
* Код основан на использованиях из `pers-grade`/`pers-static`.

## Пакеты

- `saas-java-http-client` - всё, что работает с http - http indexer, searcher, SaasDmService, общие пакеты
- `saas-java-yt-client` - работа через `yt-pull` - подготовка данных в YT, и забор их оттуда, имеет зависимости на yt, market-proto


## Как объявлять документы

Определить свой документ со списком свойств (имлементация `SaasDocument`), есть два варианта определения свойств:
1. простой, через `setProperty(name, *)` - использовался в предшественнике этой библиотеки, нужно где-то отдельно делать 
    список свойств
2. через `SaasAttr` - позволяет описать поля в классе, через конструктор, который даёт страшные generic сигнатуры типов.. 
    которые позволяют потом проверять, в какое место поле можно/нельзя засунуть (индексация, получение данных, поиск), и как его использовать.
    
## Поиск

SaasSearchService/SaasSearchRequest
- либо через `SaasSearchRequest.filterBy` - для "простых полей"
- либо через `SaasSearchRequest.addTerm` и `Term.*` операции (логика и/или/не, скобочки)

## Начало работы

Для начала работы сгенерируйте проект с помощью команды

```shell script
ya ide idea --iml-in-project-root --project-root ~/arc/idea-projects/market/jlibrary/saas-java-client
```

и откройте папку проекта в idea.
Данная подходит для структуры каталогов arc, описанной в [wiki](https://wiki.yandex-team.ru/users/sulim/howto/arc-directory-structure/).
Если вы используете другую структуру, замените `~/arc/idea-projects/market/jlibrary/saas-java-client` на нужную папку.

## Continuous delivery pipeline

Данная библиотека собирается пайплайном [market-libraries](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/market-libraries).
