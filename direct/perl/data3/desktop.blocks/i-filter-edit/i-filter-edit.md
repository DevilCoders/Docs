#i-filter-edit#

##Описание##
Общий блок, реализующий попап со списком условий для фильтра
От него наследуется b-feed-filter-edit, в будущем от него должен начать наследоваться  b-dynamic-condition-edit
Вынужденно наследуется от i-glue - потому что i-glue нужен в b-feed-filter-edit

Основные методы:
initialize - загружает конфиг и инициализирует попап
Основные методы, использующиеся в дочерних блоках
_validateConditionsList - валидирует список условий для фильтра
_getConditionsListData - получает список данных для текущего фильтра
_showConditionsListErrors - показывает ошибки, используя b-error-presenter


###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )
