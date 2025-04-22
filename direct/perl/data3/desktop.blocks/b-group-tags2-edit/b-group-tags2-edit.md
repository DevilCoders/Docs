r104222
# b-group-tags2-edit

Редактирование меток на страницах мультиредактирования (Смарт, ДО, МКБ)

## Пример
```
this._popup.setContent(BEMHTML.apply({
    block: 'b-group-tags2-edit',
    availableTags: campaignTags,
    selectedTags: (this._groupModel.get('tags') || []).map(getTagValue),
    useBanner: this._campaignModel.get('mediaType') == 'mcbanner'
}));
```

## Автор ##
[alkaline](https://staff.yandex-team.ru/alkaline)
