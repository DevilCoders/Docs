##b-edit-banner2_type_mcbanner
Блок редактирования графического баннера на поиске

Параметры блока
`
    {
        block: 'b-edit-banner2',
        mods: { type: 'mcbanner' },
        banner: {Object}, //баннер который редактируем,
        prevBanner: {Object} //предыдущий баннер (для функции "скопировать из предыдущего")
        disabledHeader: {Boolean},  //не показывать "шапку" (толстая серая полоса над баннером и номер баннера)
        group: {Object}, //группа, к которой принадлежит баннер
        canEditDomain: {Boolean}, //есть права на редактирования домена
        hasHeaderActions: {Boolean} //содержит в шапке ссылки "скопировать из предыдущего" и "очистить"
        isSingleGroup: {Boolean} //на редактировании находится только одна группа (В случае ЛИ - всегда)
        canDelete: {Boolean} //идет можно удалять баннер
    }
`

###Мейнтейнер
@alkaline
@anyakey
