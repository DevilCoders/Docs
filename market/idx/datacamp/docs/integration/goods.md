## Общая схема интеграции

Для регистрации в маркетном пространстве партнеров (получения `business_id, shop_id, feed_id`) используется MBI. Товарная Вертикаль предоставляет пользователю поиск по лучшей цене, агрегируя предложения из разных источников. В частности часть товаров для своей выдачи они приносят в DCMP сами (**чисто-ТВ** офферы), а часть - набирают из уже имеющихся (маркетных / директовых). Для генерации собственных офферов ТВ использует два источника: дикий веб (офферы, попаршенные из интернета) и фиды, которые мерчи приносят в Вебмастер (кабинет ТВ). Основной код индексатора и репорта ТВ - маркетный

Офферы, которые должны попасть на выдачу товарной вертикали, размечаются специальным флагом `vertical_approved`. Для некоторых типов офферов этот флаг может добавлять бизнес-логику: например директу не нужна индексация (а значит и майнинг), но ТВ нужна => `vertical_approved` директовые офферы обогащаются в части пайплайнов майнера. Источником разметки, а так же источником, создающим дикие чисто-ТВ офферы является [SortDC](./sortdc.md)

### Дикий веб
![vertical-wild](../_images/vertical-wild.png)

### Фиды

Во время парсинга такого фида в SortDC отправляется комплит команда с информацией о том, какие офферы / урлы в нем присутствовали. Эту информацию SortDC использует для изменения разметки `vertical_approved`.

Т.к. в фидах, приносимых ТВ-партнерами, может быть много нерелевантных офферов, не все из них кладется в стейт. Во время парсинга чисто-ТВ фидов парсер проверяет, есть ли в стейте "заглушка" от SortDC - пустой оффер, хранящий идетификаторы и `vertical_approved` флаг. Если заглушка есть, оффер отправляется в стейт, иначе выкидывается прямо на этапе парсинга

![vertical-feed](../_images/vertical-feed.png)
