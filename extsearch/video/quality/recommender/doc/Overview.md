## Как работают рекомендации в ВХ

Для понимания написанного в этой документации читателю понадобятся базовые знания аппхоста ([тыц](https://wiki.yandex-team.ru/apphost/)), поискового стека ([тыц](https://doc.yandex-team.ru/Search/ySearchArchIntro/concepts/About.html)) и рекомендательной платформы DJ ([тыц](https://a.yandex-team.ru/arc/trunk/arcadia/dj/doc/Overview.md)).

#### Как в нас идут

Клиенты обычно ходят в нас не напрямую, а через прокси-ручки frontend.vh:

feed

`curl 'https://frontend.vh.yandex.ru/v23/feed.json?limit=10&offset=0&filter=carousels&num_docs=20&delete_filtered=0&synchronous_scheme=1&locale=ru&from=efir&reqid=1572114050.2644.121996.293586&service=ya-main&disable_trackings=1'`

и carousel

`curl 'https://frontend.vh.yandex.ru/v23/carousel_videohub.json?carousel_id=CATEG_FILM&limit=20&offset=0&delete_filtered=0&locale=ru&from=efir&reqid=1572114050.2644.121996.293586&service=ya-main&disable_trackings=1'`​ .

Первая идет за всеми каруселями сразу (опционально может идти за миксером - см. эфир на тачах), а вторая обычно используется, чтобы показать лендинг или дозапросить документы в карусели. Эти прокси обогащают наш ответ сниппетами и мета-информацией, применяют быстрые баны.

Примеры таких запросов можно выдрать из дебажной консоли браузера. Там же можно найти аппхостовый и поисковый reqid, по которым можно потрейсить запрос.

#### Аппхост

Ручки frontend.vh идут в нашу ручку video/videohub через аппхост. Аппхостовый граф этой ручки можно найти вот [тут](https://apphost.n.yandex-team.ru/#/graph/production/VIDEO::videohub). Для дебага часто бывает удобно сходить в ручку через http-adapter, это можно сделать, например, вот так:

`video-http-apphost.yandex.ru/video/videohub?client=vh&enable_svod_for_all=1&is_ya_plus=1&limit=18&locale=ru&num_docs=20&offset=0&puid=135682275&rearr=scheme_Local/FilterBannedVideo/SvodForAll%3D1;scheme_Local/VideoSvodMiddle/maxSvodCount%3D10;scheme_Local/VideoSvodUpper/SvodMaxCount%3D10&region=225&relev=should_show_svod%3D1&request=sport_hockey_league_nhl&vitrina_categ_order=user&vitrina_cold_start=enable&vitrina_filter=vh&ya_plus_type=YA_PREMIUM&yandexuid=918509751531753849`

В целом граф работает следующим образом:

* Инициализирует параметры запроса
* Идет в блэкбокс с кукой, чтобы получить индентификаторы пользователя
* Получает профиль пользователя из FPS'а (про него подробнее ниже), который обращается к kvSaaS и RTMR.
* Идет с профилем в разные источники рекомендаций - средние свежести, вх и видео, RTX (сервис для эксплорейшена), ОО (он же entity, объектный ответ), досмотр
* Мержит ответы источников в блендере
* Постпроцессит и отдает ответ

Код наших сетапов можно найти вот [тут](https://a.yandex-team.ru/arc/trunk/arcadia/web/src_setup/lib/setup) в папках videohub, videohub_apphost и videohub_init; а вот [тут](wiki.yandex-team.ru/users/justdev/Kak-podnjat-srcsetup/) лежит инструкция о том, как их поднять.

#### FPS

FPS (Fresh Profile Server) - это диджейная компонента (поддерживает походы по хттп и аппхост), которая позволяет получать профили диджейных объектов.

В целом FPS работает следующим образом:

1. Идет в статическое хранилище (обычно kvSaaS) и/или динамическое хранилище (чаще всего YDB или RTMR) за профилями по полученному ключу или ключам.

   Несколько ключей в одном запросе может понадобиться, например, тогда, когда мы хотим получить профили сразу нескольких разных идентификаторов пользователя таких, как, например, puid и yandexuid.

   Ключ имеет формат `$prefix/$namespace_id#$type_id/$object_id`.  В нашем инстансе FPS'а этот префикс всегда пустой. Таким образом, для получения, например, профиля видео-документа, который имеет диджейный тип объекта `PN_Video#OT_DOCUMENT`, ключ должен иметь вид `/9#1/$url`, где 9 и 1 - это значения `PN_Video` и `OT_DOCUMENT` в соответствующих энумах, а $url - это URL документа.

2. После получения профилей из всех хранилищ они мержатся стандартными средствами DJ, получившийся профиль после этого редьюсится на текущий таймстемп.
3. К поредьюшенному профилю применяются некоторые DJ-правила типа ModifyProfile.

Наш FPS живет в няне в 4 инстансах ([дев](https://nanny.yandex-team.ru/ui/#/services/catalog/vla_vitrina_fresh_profile_server_dev/), [вла](https://nanny.yandex-team.ru/ui/#/services/catalog/vla_vitrina_fresh_profile_server/), [ман](https://nanny.yandex-team.ru/ui/#/services/catalog/man_vitrina_fresh_profile_server/), [сас](https://nanny.yandex-team.ru/ui/#/services/catalog/sas_vitrina_fresh_profile_server/)). Конфиги фпса живут вот [тут](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/video/quality/recommender/dj/rules/fresh_profile_server.conf).

В качестве статического хранилища в видеохостинге используется kvSaaS, а в качестве динамического - RTMR, в этом можно убедиться, посмотрев на конфиги в няне.

#### kvSaaS-профили

kvSaaS - это key/value-хранилище на базе SaaS (Search-as-a-Service). Документация по нему живет вот [тут](https://wiki.yandex-team.ru/jandekspoisk/SaaS/). Мы постоянно (не реже, чем раз в сутки) обновляем данные в этом хранилище, кладя туда профили пользователей, документов, тэгов и других объектов с самыми свежими изменениями.


