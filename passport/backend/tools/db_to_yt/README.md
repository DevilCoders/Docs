## Выгрузка бд паспорта в YT
### family_admin
[Ссылка на таблицу на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/passport/production/family_admin)

Структура:
`admin_uid`, `family_id`

### unsubscribed_from_maillists
[Ссылка на таблицу на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/passport/production/unsubscribed_from_maillists)

Структура:
- `uid`: целочисленный
- `unsubscribed_from_maillists` ∈ `{"all", "1,2,3,4,...,N"}`

### is_child
[Ссылка на таблицу на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/passport/production/is_child)

В таблицу входят только детские аккаунты (то есть для них задан атрибут 210 в blackbox)

Структура:
- `uid`
