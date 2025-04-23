//r106561
##b-edit-banner2_type_text
Блок редактирования ТГО баннера

Параметры блока
`
    {
        block: 'b-edit-banner2',
        mods: { type: 'text' },
        banner: {Object}, //баннер который редактируем,
        prevBanner: {Object} //предыдущий баннер (для функции "скопировать из предыдущего")
        disabledHeader: {Boolean},  //не показывать "шапку" (толстая серая полоса над баннером и номер баннера)
        group: {Object}, //группа, к которой принадлежит баннер
        withVCard: {Boolean}, //содержит редактирование визитки
        canEditDomain: {Boolean}, //есть права на редактирования домена
        hasHeaderActions: {Boolean} //содержит в шапке ссылки "скопировать из предыдущего" и "очистить"
        isSingleGroup: {Boolean} //на редактировании находится только одна группа (В случае ЛИ - всегда)
        canDelete: {Boolean} //идет можно удалять баннер
    }
`

Для нормальной работы частей блока ему нужны два сторонних попапа:

###Попап выбора изображений
  `
    block: 'b-outboard-controls',
    js: { id: 'pic-selector-control' },
    attrs: { id: 'pic-selector-control' },
    content: {
        elem: 'popup',
        innerBlock: {
            block: 'b-pic-selector'
        },
        buttons: false,
        header: false,
        innerBlock: b-pic-selector
    }
 `

###Попап выбора сайтлинков

`
    block: 'b-outboard-controls',
    js: { id: 'sitelinks-selector-control' },
    attrs: { id: 'sitelinks-selector-control' },
    content: {
        elem: 'popup',
        innerBlock: {
            block: 'b-sitelinks-selector',
        },
        buttons: {
            block: 'b-sitelinks-selector',
            mods: { mode: 'banner' },
            js: { id: 'multiedit-sitelinks-selector' },
            modelId: 'banner',
            content: { elem: 'buttons' }
        }
    }
`

###Мейнтейнер
@anyakey
