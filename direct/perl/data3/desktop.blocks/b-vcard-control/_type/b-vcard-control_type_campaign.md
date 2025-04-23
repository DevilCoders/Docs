# Блок для вывода визитки
Используется на странице на странице параметров кампании

## Пример
```
{
    block: 'b-vcard-control',
    mods: { type: 'campaign' },
    vcardHint: '&nbsp;',
    is_vcard_open: campaign.camp_with_common_ci,
    vcard: (campaign && campaign.vcard) || {}
}
```
