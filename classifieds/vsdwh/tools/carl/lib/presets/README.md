# Пресеты

**Пресеты** — это функции для описания типовых графов. Если команда регулярно делает плюс-минус одинаковые графы, делающие по смыслу примерно одно и то же, и которые легко параметризовать относительно небольшим числом аргументов, то имеет смысл определить для него пресет, что позволит избежать копипастинга, унифицировать такие процессы внутри команд и сделать разработку графов проще и быстрее.

С точки зрения пользователя `carl` пресет при описании графов кодом полностью аналогичен vh3-операциям и подграфом: его точно так же надо импортировать из соответствующего пакета и вызывать с нужными аргументами внутри функции `workflow`. Примеры использования пресетов есть в [examples](../../examples).

Идейно пресеты вдохновлены пресетами [lama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama), позволяющими создавать однотипные реакции в несколько строк.


## Разработка собственных пресетов
По сути описание операций внутри пресета ничем не отличается от описания собственного графа `carl`-кодом внутри функции `workflow`, кроме того, что пресет принимает большее число аргументов на вход.

Пресеты также, как и [подграфы](../operations/subgraph) считаются узконаправленными объектами, специфичными для команд, поэтому структура для их хранения тоже проектная. Строгих рекомендаций для описания пресетов, помимо места их хранения, нет, внутри функции может быть реализована любая логика добавления любых операций из [библиотеки операций carl](../operations) в зависимости от переданных аргументов. Однако, не предполагается, что функция-пресет будет возвращать что-то кроме `None`, и не предполагается, что в `carl`-коде внутри функции `workflow` будут использоваться какие-то vh3-операции помимо самого пресета, то есть пресет должен представлять граф целиком и не нуждаться в дополнениях. Конечно, пресет можно создать со входами и выходами, но в таком случае "несамостоятельности" пресета стоит рассмотреть другие варианты, потому что в таком случае описываемая сущность уже больше походит по смыслу на подграф или композитную операцию.

### Обязательные требования к пресетам:
* Расположение в директории проекта вашей команды внутри [projects](projects)
* Названия пресета, его внутренних методов и переменных не должны содержать слова `workflow`, т.к. это имя зарезервировано для описания графа в верхнеуровневом конфиге
* Ресурсы пресетов и источники кода добавляются только в локальный [ya.make](./ya.make) пресетов
### Рекомендации:
* Рекомендуется вносить импорты пресетов и сами пресеты в `__all__` внутри `__init__.py` пакета вашего проекта для облегчения импортировать.
* Крайне желательно снабжать свои пресеты описаниями по аналогии с представленными в проекте [vertis_dwh](projects/vertis_dwh). На аргументы пресета можно завязать много логики, описание аргументов и логики взаимодействия с ними, поможет проще использовать пресет коллегам.
* Если пресет использует какие-то однотипные данные (например, какой-нибудь параметризованный шаблон запроса), можно хранить его в ресурсах рядом с пресетом и подгружать значение из него функцией `resource_opt`/`expr_resource_opt` из утилит операций.
* В будущем планируется функционал автоматического обновления графов, использующих какой-либо пресет, при измененияъ этого пресета. Поэтому рекомендуется хранить один пресет в одном `.py` файле с таким же именем, как и у функции-пресета.
