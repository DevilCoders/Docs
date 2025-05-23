# Код отчетов

Основные требования к коду:
* хорошо декомпозирован
* легко расширяем
* легкий в понимании
* повторно используемый

## Сущности

__Flow__ - похож на абстрактный класс или интерфейс. Без реализации описываем как это должно работать. Описание алгоритма, который превращает бизнес требования в бизнес логику

__Method__ — готовая бизнес логика. Разделяется на 2 вида.
1. Самая примитивная логика, которая не требует для себя описания flow.

2. Бизнес логика, которая получена из flow, при передаче ему других методов. Похож на обычный класс. Берем абстрактный класс и натягиваем на него реализацию.

## Каким проблемы решает

* __Декомпозиция.__ Flow позволяет и помогает разрабатывать функциональность независимо. Общий алгоритм всей системы можно описать не имея готовой реализации ее частей.

* __Расширяемость.__ Можно безболезненно дополнять и изменять flow, так как конечная реализация бизнес логики находится в методах.

* __Повторное использование.__ Flow можно переиспользовать для разных частей приложения. Нужно просто передать нужную реализация через методы.

* __Читаемость.__ Flow только описывает логику, самой бизнес логики там нет. Это облегчает понимание происходящего там.

## Немного для понимания философии данного подхода

Бизнес требования формируют техническую задачу, которая имеет свой алгоритм решения. В ходе возникновения новых бизнес требований, формулировка технических заданий может меняться. Эти изменения могут потребовать изменений в структуре кода, если алгоритм решения новой технической задачи стал другим.

Чтобы работать с этим было проще и разработчики, из-за боязни поломать что-то из-за изменения алгоритма, не писали костыли, решено было описание алгоритма работы приложения выносить отдельно в сущность под название flow.

## Примеры решения большинства задач

* Создание flow с зависимостями между методами. [Пример похода в апи](./modules/api/flows/request.ts)
* Создание flow поверх другого flow:
    1. Можно позаимствовать описание типов наследуемого flow. [Пример](./modules/url/flows/report.ts)
    2. Можно не наследовать flow, а передать его как отдельный метод. [Пример](./modules/segmentation/methods/report.ts)
