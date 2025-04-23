## Параметры партнёрской программы

-   `affiliate_clid` - ID партнера в Дистрибуции, уникальный для каждого партнера
-   `admitad_uid` - Уникальный идентификатор партнёра (в системе Admitad), который содержится во всех партнёрских ссылках
-   `travelpayouts_uid` - Уникальный идентификатор партнёра (в системе Travelpayouts), который содержится во всех партнёрских ссылках. Аналогично admitad_uid, только для TravelPayouts. В него же через `.` добавляется дополнительный маркер для статистики
-   `affiliate_vid` - Дополнительный маркер для статистики, отсутствует у Travelpayouts, т.к. входит в состав `travelpayouts_uid`

## Сочетание параметров

| Партнёр            | `affiliate_clid` | `admitad_uid` | `travelpayouts_uid` | `affiliate_vid` |
| ------------------ | ---------------- | :-----------: | :-----------------: | :-------------: |
| Admitad            | `affiliate_clid` | `admitad_uid` |          -          | `affiliate_vid` |
| Travelpayouts      | `affiliate_clid` |       -       | `travelpayouts_uid` |        -        |
| Яндекс.Дистрибуция | `affiliate_clid` |       -       |          -          | `affiliate_vid` |

## Куда пишутся параметры

В данный момент параметры передаются вмсете с атрибуцией в следующие ручки:

-   `/search_hotels/`
-   `/get_similar_hotels/`
-   `/get_hotel_offers/`
-   `/get_hotel_info/`
