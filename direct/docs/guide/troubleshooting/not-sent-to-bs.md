# Не отправляется в БК

В этой инструкции описываем типовые ситуации почему объекты могут не отправляться в БК и какие условия следует проверить.

_Страничка не претендует на полноту, будем дописывать по ситуации._

## Ничего не отправляется
### Общий счет был в БК
Если у кампании `wallet_cid` != 0, то у кампании—кошелька должен быть `OrderID` > 0.

### Кампания промодерирована
Убедиться, что:
- `campaigns.statusModerate` = `Yes`
- `camp_options.statusPostModerate` = `Accepted`

### На кампании есть деньги
Если кампания еще не была в БК (`OrderID` = 0), то на ней или кошельке должен быть положительный остаток

## Не отправляется группа целиком
Отправляем в БК — кампания отправляется, а группа — нет.

### Что-то не промодерировано
Проверить, что у объектов статусы модерации — `Yes`:
- `phrases`:
   - `statusModerate`
   - `statusPostModerate`
- `bids`: `statusModerate`
- `banners`:
   - `statusModerate`
   - `statusPostModerate`
   - `phoneflag` (если нет ссылки и есть визитка)
   - если есть сайтлинки, то `statusSitelinksModerate` должен быть `Yes` или `No` ([пруф](https://st.yandex-team.ru/DIRECT-12360#53d74221e4b0355d28287d4e))

### Минус регионы
Минус-регионы на баннере могут вычитаться с таргетингом группы.
Стоит проверить что регионы в `banners_minus_geo` для всех баннеров группы не вычитают полностью геотаргетинг группы `phrases.geo`.

Еще возможны пограничные ситуации с неконсистентными статусами отправки баннера / группы / минус-регионов в БК, но без конкретного примера под рукой — не опишу.
Помогает переотправить в БК одновременно группу и все баннеры.

### Ретаргетинг содержит недоступные цели
Если в группе только условия ретаргетинга — нужно проверять, что они не содержат целей с `retargeting_goals.is_accessible` = 0.
