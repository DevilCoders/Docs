#i-filter-edit__validator#

##Описание##
Блок для валидации условий в фильтрах

###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )

##Пример##

`
    u['i-filter-edit__validator'].validate(ruleType, value);

`
Поддерживаемые типы валидации:

 'number'  => { checker => '_check_number', avalible_constraints => [qw/maxValue minValue/] },
 'integer' => { checker => '_check_int', avalible_constraints => [qw/maxValue minValue/] },
 'string'  => { checker => '_check_string', avalible_constraints => [qw/maxLength minLength withoutSpaces/]},
 'object'  => { checker => '_check_object', avalible_constraints => [qw//]},
 'array'   => { checker => '_check_array',  avalible_constraints => [qw/itemsCountMax itemsCountMin itemAnyOf/]},
 'range'   => { checker => '_check_range', avalible_constraints => [qw/leftLessRight/] },

