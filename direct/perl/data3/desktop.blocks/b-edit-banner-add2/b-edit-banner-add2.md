## b-edit-banner-add2 ##
Блок кнопки добавления объявления.
Умеет отображать количество объявлений, которые еще можно добавить и дизейблится, когда лимит достигнут
Выглядит [вот так](https://jing.yandex-team.ru/files/alkaline/Redaktirovanie_gruppy_objyavlenii_2017-01-25_13-55-37.png)

## Пример ##
`
    {
        block: 'b-edit-banner-add2',
        mainTitle: iget('Добавить баннер'),
        pluralTitles: [iget('баннер'), iget('баннера'), iget('баннеров')],
        availableToCreateBannersCount: u.consts('DEFAULT_CREATIVE_COUNT_LIMIT') - group.banners_quantity,
        bannersLimit: u.consts('DEFAULT_CREATIVE_COUNT_LIMIT')
    }
`

## Мейнтенеры ##
@alkaline
