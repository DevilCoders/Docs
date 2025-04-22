r107790

## b-dynamic-media-creatives-choose ##
Блок выбора креатива из хранилища креативов.__
Используется на странице мультиредактирования динамических медийных групп
Имеет 2 модификации: `_type_add` и `_type_edit`, для массового выбора(с чекбоксами) и единичного(с радиобоксом) соответственно

Выглядит [вот так](http://jing.yandex-team.ru/files/alkaline/2015-09-18_1632.png).

## Пример ##
    {
        block: 'b-dynamic-media-creatives-choose',
        mods: { type: 'add' },
        ulogin: u.consts('ulogin'),
        limit: u.consts('DEFAULT_CREATIVE_COUNT_LIMIT')
    }
