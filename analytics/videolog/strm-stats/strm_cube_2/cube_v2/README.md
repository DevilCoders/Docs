# Кубы видеосмотрения
Выжимки из логов, касающихся смотрения видео и рекламы на видеохостинге Яндекса.  
Лежат на Хане в папке [//cubes/video-strm](https://yt.yandex-team.ru/hahn/#page=navigation&path=//cubes/video-strm). Сами кубы лежат в табличках `//cubes/video-strm/YYYY-MM-DD/sessions`, в `/preprocessed` табличках, которые хранятся недолго — итоги предварительных мапов исходных логов для быстрых пересчётов.

Процесс, который собирает кубы: https://hitman.yandex-team.ru/projects/strm_stats_nc/strm_cube_3_sessions

Логи, информация из которых содержится в кубах:
1. [//logs/strm-access-log](https://yt.yandex-team.ru/hahn/#page=navigation&path=//logs/strm-access-log) — лог бэкенда, запросы за плейлистами и чанками
2. [//logs/strm-gogol-log](https://yt.yandex-team.ru/hahn/#page=navigation&path=//logs/strm-gogol-log) / [//logs/jstracer-log](https://yt.yandex-team.ru/hahn/#page=navigation&path=//logs/jstracer-log) — лог, который отсылает плеер
3. [//logs/redir-log](https://yt.yandex-team.ru/hahn/#page=navigation&path=//logs/redir-log) — дублирующее gogol логирование на серпе и некоторых других сервисах
4. [//statbox/cooked_logs/bs-dsp-cooked-log](https://yt.yandex-team.ru/hahn/navigation?path=//statbox/cooked_logs/bs-dsp-cooked-log&), [//statbox/cooked_logs/bs-chevent-cooked-log](https://yt.yandex-team.ru/hahn/navigation?path=//statbox/cooked_logs/bs-chevent-cooked-log&), [//logs/awaps-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/awaps-log/1d&), [//logs/bs-chtracking-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/bs-chtracking-log/1d&) — рекламные логи
5. [//logs/yandex-access-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/yandex-access-log/1d&), [//logs/morda-access-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/morda-access-log/1d&), [//logs/news-scarab-access-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/news-scarab-access-log/1d&), [//home/answers/yuid_testids](https://yt.yandex-team.ru/hahn/navigation?path=//home/answers/yuid_testids&), [//logs/zen-events-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/zen-events-log/1d&), [//home/alice/dialog/prepared\_logs\_expboxes](https://yt.yandex-team.ru/hahn/navigation?path=//home/alice/dialog/prepared_logs_expboxes&) — информация о тестидах
6. [//home/antifraud/export/videohosting/views](https://yt.yandex-team.ru/hahn/navigation?path=//home/antifraud/export/videohosting/views&) — антифрод

И отдельные таблицы:
1. [//home/videolog/strm\_meta/iron\_branch/concat](https://yt.yandex-team.ru/hahn/navigation?path=//home/videolog/strm_meta/iron_branch/concat&) — метаинформация о видеороликах
2. [//home/crypta/production/profiles/export/profiles\_for\_14days](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/profiles_for_14days&) — соц-дем из Крипты
3. [//home/videolog/24julia/mma-2177/1.efir_history](https://yt.yandex-team.ru/hahn/navigation?path=//home/videolog/24julia/mma-2177/1.efir_history&) — retention Эфира по яндексуидам
4. [//home/videolog/strm\_meta/yandexuids\_subscriptions](https://yt.yandex-team.ru/hahn/navigation?path=//home/videolog/strm_meta/yandexuids_subscriptions&) — подписки яндексуидов

## Что есть в логе + примеры YQL
### Как устроены кубы
Одна строчка представляет собой непрерывное смотрение **в одном экземпляре плеера одной единицы контента**. Назовём такое смотрение **микросессией**. Плеер идентифицируется по уникальному идентификатору **vsid** (VideoSessionID), который выдаётся в момент инициализации плеера. Контент идентифицируется по полю **videoContentId** в исходных логах (соответствует колонке **video_content_id** в кубах).

Пример: пользователь пришёл, посмотрел фильм 1 до середины, потом, не перезагружая плеер, переключился на фильм 2, затем вернулся к фильму 1 и досмотрел его, также не перезагружая плеер. Несмотря на то, что идентификатор плеера не менялся, такому смотрению будут соответствовать три строчки в кубах.
### Самое важное
view_time — время смотрения в секундах
price — деньги в миллионных долях рубля (price / 1000000.0 — деньги в рублях)
### По колонкам
#### ad_events (any?)
Список YSON-словарей. Все рекламные события, которые были в сессии. Пример:
```
{
    "BidReqid" = "3369678799065880993";
    "BrowserName" = "YandexBrowser";
    "DetailedDeviceType" = "Windows";
    "DeviceType" = 5;
    "DspID" = 1;
    "Hit" = 0;
    "PageID" = "344438";
    "PartnerPrice" = 0;
    "Price" = 0;
    "RegionId" = 10748;
    "RequestId" = "3369678823183653281";
    "ShownHit" = 0;
    "UniqID" = 5741692971592329918;
    "ad_type" = "instream";
    "adsessionid" = "0";
    "bidid" = 3369678799075580321;
    "campaignid" = 32007062;
    "countertype" = 0;
    "imp_id" = "8";
    "is_vh" = %true;
    "maxadscount" = 1;
    "overlay" = %false;
    "partner_name" = "kp.ru";
    "partnerprice" = 25870;
    "position" = 3;
    "price" = 51740;
    "producttype" = "video-motion";
    "timestamp" = 1592332704;
    "video_type" = "preroll";
    "videoduration" = 10;
    "win" = 0
};
```
Отфильтровать винхиты (ролики, отобранные для показа) и собственно показы можно так:
```
$isShow = ($x)->(
    Yson::LookupInt64($x, "countertype") == 1
    and Yson::LookupInt64($x, "win") == 1
    and Yson::LookupInt64($x, "DspID") not in (5, 10)
);

$isWinhit = ($x)->(
    Yson::LookupInt64($x, "countertype") == 0
    and Yson::LookupInt64($x, "win") == 1
    and Yson::LookupInt64($x, "DspID") not in (5, 10)
);

select
ListFilter(Yson::ConvertToList(ad_events), $isWinhit) as winhits,
ListFilter(Yson::ConvertToList(ad_events), $isShow) as shows,
```
В колонку **price** вынесена сумма поля price (`Yson::LookupInt64($x, "price")`) по словарям из списка, а в **partner_price**, соответственно — поля partner_price.
#### ad_tracking_events (any?)
Список YSON-словарей. События трекинга рекламы (клики, скипы) из awaps и chtracking логов. Пример:
```
 {
    "action" = "midpoint";
    "bidid" = 3369678799075580321;
    "campaignid" = 32692547;
    "source" = "chtracking";
    "timestamp" = 1592332715
};
```
#### add_info (any?)
YSON-словарь с дополнительной информацией о сессии. Оно большое и как правило в расчётах не нужно, но иногда помогает. Вероятно, наиболее интересные в нём поля `%columnname%_counter`, где можно увидеть, из каких логов и какие значения приехали в колонку `%columnname%`.
Пример:
```
"ip_counter" = {
    "js_tracer" = {
        "85.141.151.3" = 187
    };
    "rtb-dsp" = {};
    "strm" = {
        "2a02:6b8:c08:a106:0:495f:a5a5:0" = 1;
        "2a02:6b8:c16:f8f:0:495f:7d85:0" = 1;
        "2a02:6b8:c1c:48f:0:495f:427f:0" = 1;
        "85.141.151.3" = 191
    }
};
```
Тут видно, что из gogol/jstracer-логов приехал ip `85.141.151.3`, а из strm-access-log — помимо него, несколько ipv6.

Начиная с 2020-08-11 в `add_info` в поле `utm_data` также лежит информация о utm-метках, если они были переданы в cgi-параметрах при создании плеера.

```
"utm_data" = {
    "utm_content" = "INTid|0100000020529058536_|cid|51114303|gid|4182614448|aid|8992375169|pos|premium1|src|search_none|dvc|desktop|kpid|0";
    "utm_term" = "кинопоиск";
    "yclid" = "4633724548941908844"
};
```

#### age_segments (any?)
Распределение вероятностей по пяти возрастным сегментам из Крипты. Пример
```
{
    "0_17" = 0.05917412042617798;
    "18_24" = 0.18897949159145355;
    "25_34" = 0.35188204050064087;
    "35_44" = 0.21101339161396027;
    "45_99" = 0.18895093351602554
}
```
#### avglogs (double?)
Показатель того, насколько хорошо плеер утилизирует доступное устройству разрешение (на маленьких экранах не нужно показывать 1080p). Рассчитывается [так](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/videolog/strm-stats/strm_cube_2/cube_v2/microsessions_reducer.py?rev=6985869#L373-374).
#### browser_name (string?)
Семейство браузера
#### browser_version (string?)
Версия браузера
#### bytes_sent (uint64?)
Количество байт скачанных в сессии чанков и плейлистов. Не учитываются рекламные чанки, так что трафик честно посчитать по этому полю нельзя.
#### category_id (string?)
ID категории из рекламных логов
#### channel (string?)
Эфирный канал, соответствует полю computed_channel в iron_branch
#### channel_id (string?)
Эфирный числовой ID канала (например, персональный канал — `1550142789`)
#### channel_old (string?)
Идентификатор бакета (для vod-ов) или техническое имя канала (для лайвов)
#### chunks_types (string?)
Расширения чанков, скачанные в сессии, через запятую
#### content_duration (int64?)
Длительность контента (если указана в метаданных в iron_branch)
#### ContentTypeID (uint64?)
ContentTypeID из iron_branch, только для старой базы контента
#### country (string?)
двухсимвольный идентификатор страны (например, `RU`). Соответствует `Geo::RoundRegionById(region_id, "country").short_en_name`
#### device_id (string?)
Идентификатор мобильного девайса (для станций etc)
#### device_type (string?)
Тип девайса по юзерагенту, допустимые значения — `desktop`, `tv`, `tablet`, `phone`.
#### efir_first_visit (string?)
Дата первого визита яндексуида в Эфир из таблички efir_history
#### efir_last_month_active_days (int64?)
Количество дней из последних 30, в которые пользователь заходил в Эфир, из таблички efir_history
#### errors (any?)
Список YSON-словарей. Ошибки и столды (ребуферинги, зависания), случившиеся во время сессии.
Когда зависание только начало происходить, кидается событие Stalled с duration=0. Столду соответствует причина (reason) (Init — в начале, Seek — из-за перемотки, AdEnd — в конце рекламы, Other — непонятно почему), длительность (stalledDuration), и Id — цифровой идентификатор столда в сессии, начиная с единицы. Если зависание длинное, дальше кидаются Stalled с duration=1, 5, 10. В конце зависания кидается StalledEnd, где записана точная длительность в секундах. Таким образом одному зависанию соответствует от двух событий. Пример столда и его StalledEnd:
```
[
    {
        "details" = {
            "connection" = "UNKNOWN";
            "isMuted" = %false;
            "reason" = "Init";
            "stalledDuration" = 0;
            "stalledId" = 1
        };
        "id" = "Stalled_Init";
        "id_raw" = "Stalled";
        "rel_time" = 1;
        "resolution" = "start";
        "source" = "js_tracer"
    };
    {
        "details" = {
            "connection" = "OK";
            "isMuted" = %false;
            "reason" = "Init";
            "stalledDuration" = 0.31726999999955297;
            "stalledId" = 1
        };
        "id" = "StalledEnd";
        "id_raw" = "StalledEnd";
        "rel_time" = 1;
        "resolution" = "start";
        "source" = "js_tracer"
    }
]
```
по stalledId (есть только в новых версиях плеера) можно склеить столд и соответствующий ему StalledEnd. Если нет цели считать длительность столда точно, а гранулярность <1сек/1сек/5сек/10сек устраивает, можно использовать следующий YQL:
```
$getStalleds = ($errors) -> {
    $errors = Yson::ConvertToList($errors);
    $stalleds = ListFilter(
        Yson::ConvertToList($errors), ($x)->(Yson::LookupString($x, "id_raw") == "Stalled")
    );
    $stalleds = ListMap(
        $stalleds, ($x)->(
            AsStruct(
                Yson::ConvertToString(Yson::YPath($x, "/details/reason")) as reason,
                Yson::ConvertToDouble(Yson::YPath($x, "/details/stalledDuration")) ?? Yson::ConvertToInt64(Yson::YPath($x, "/details/stalledDuration")) as duration,
                $wrapBool(Yson::ConvertToBool(Yson::YPath($x, "/details/isMuted"))) as muted_cat,
            )
        )
    );
    $stalleds = $dedup_stalleds($stalleds)
    return $stalleds
}

select $getStalleds(errors)
```
Пример ошибки:
```
{
    "details" = {};
    "id" = "shaka.TIMEOUT_1003_MANIFEST_fatal";
    "id_raw" = "shaka.TIMEOUT_1003_MANIFEST";
    "rel_time" = 77;
    "resolution" = "start";
    "source" = "js_tracer"
};
```
Если id заканчивается на `_fatal`, то ошибка фатальная, после неё проигрывание не может продолжаться (но плеер ещё пытается перезагрузить себя).
#### exact_socdem (any?)
YSON-словарь. Соцдем-показатели из Крипты, уже в форме «выбраны наиболее вероятные сегменты по каждому показателю». Пример:
```
{
    "age_segment" = "45_54";
    "gender" = "m";
    "income_5_segment" = "B1";
    "income_segment" = "B"
}
```
#### fielddate (string)
Дата, за которую логи, в `yyyy-mm-dd`.
#### fraud (uint64?)
Приджойненный по яндексуиду показатель фродовости, 0 или 1. Если 1 — то фрод
#### gender (any?)
Вероятности пола пользователя из крипты. Пример:
```
{
    "f" = 0.922;
    "m" = 0.078
}
```
#### gogol_service (string?)
Значение поля service из gogol-лога. 
`StreamPlayer` — веб-плеер  
`ott-smart` — смарттв-приложения Кинопоиска  
`AndroidPlayer` — встраиваемый андроидный плеер  
`YandexMusic` — приложение яндекс-музыки  
`ApplePlayer` — ios-плеер  
`iosZenAppPlayer` — дзеновский ios-плеер  
`AdSDKJS` — рекламный плеер на вебе
#### heartbeats (any?)
YSON-словарь, где записано, сколько хартбитов и из каких логов они приехали. Пример:
```
{
    "js_tracer" = {
        "10SecWatched" = 1;
        "20SecWatched" = 1;
        "30SecHeartbeat" = 8
    };
    "redir" = {
        "redir_heartbeat" = 8
    }
}
```
#### heur_category (string?)
Два значения — `live_or_catchup` и `vod`. Посчитано эвристически, т.ч. может не совпадать с реальностью.
#### hits_block_good (int64?)
Количество блоков рекламных хитов
#### hits_good (int64?)
Количество рекламных хитов
#### icookie (string?)
Кука icookie
#### income_segments (any?)
Вероятности сегментов дохода пользователя из Крипты. Пример:
```
{
    "A" = 0.07430031150579453;
    "B" = 0.5820541381835938;
    "C" = 0.3436455801129341
}
```
#### ip (string?)
ip-адрес
#### is_dhd (string?)
Является ли видео DeepHD, варианты — `dhd`, `not_dhd`, `unknown`
#### is_kal (string?)
`is_kal == "kal"` — более надёжный идентификатор того, что просмотр был лайвом, чем heur_category
#### license (string?)
Лицензия контента: NULL/Avod — доступно без лицензии, Svod — доступно по подписке, Tvod_Est — доступно для покупки
#### os_family (string?)
Семейство OS из юзерагента
#### page_id (string?)
Рекламный идентификатор, примерно соответствующий сервису, на котором показывается реклама (но не всегда, может соответствовать и контенту)
#### ParentTypeID (uint64?)
ParentTypeID из iron_branch, только для старой базы контента
#### ParentUUID (string?)
UUID родителя из iron_branch, только для старой базы контента
#### partner_price (int64?)
Количество денег в миллионных долях рубля, которое мы отдаём партнёру
#### player_alive_data (any?)
YSON-словарь. Данные из событий PlayerAlive, по категориям разрешения (ld, sd, hd, fhd) и вместе. Пример:
```
{
    "ld" = {
        "stalledCount" = 1;
        "stalledTime" = 0.8994999999995343;
        "watchedTime" = 4.06;
        "watchedTimeNonMuted" = 4.06;
        "watchedTimeVisible" = 4.06;
        "watchedTimeVisibleNonMuted" = 4.06
    };
    "sd" = {
        "stalledCount" = 0;
        "stalledTime" = 0;
        "watchedTime" = 3.0920000000000005;
        "watchedTimeNonMuted" = 3.0920000000000005;
        "watchedTimeVisible" = 3.0920000000000005;
        "watchedTimeVisibleNonMuted" = 3.0920000000000005
    };
    "total_stalled_count" = 1;
    "total_stalled_time" = 0.8994999999995343;
    "total_view_time" = 7.152;
    "total_view_time_non_muted" = 7.152;
    "total_view_time_visible" = 7.152;
    "total_view_time_visible_non_muted" = 7.152
}
```
Содержит информацию о времени просмотра, количестве и общей длительности столдов.
#### player_events (any?)
Список YSON-словарей. Формат такой же, как у поля errors. Плеерные события, не являющиеся ошибками.
#### player_version (string?)
Версия плеера.
#### playlists_types (string?)
Расширения плейлистов, скачанные в сессии, через запятую
#### price (int64?)
Количество денег в миллионных долях рубля, которое мы заработали за рекламу на этой сессии
#### program (string?)
Тайтл «программы» (в модели канал-программа), или просто проигрываемого контента. Соответствует полю `computed_program` из iron_branch
#### provider (string?)
Провайдер пользователя, вывод функции Geo::GetIspNameByIp.
#### puid (string?)
Паспортный ID (если есть)
#### ref_from (string?)
Идентификатор сервиса, присылаемый в логи в поле from. Посмотреть соответствия реальным сервисам можно [тут](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/videolog/strm-stats/strm_cube_2/stability/stability_common.sql?rev=6881810#L70)
#### ref_from_block (string?)
Идентификатор блока на сервисе, с которого началось смотрение у пользователя, присылаемый в поле from_block. Есть не на всех сервисах.
#### region (int64?)
#### reqid (string?)
Идентификатор запроса, есть на новостях, серпе, видео, погоде, эфире, турбо.
#### selfpromo_events (any?)
События selfpromo — когда на наших сервисах рекламируются другие наши сервисы. Показывается вместо/вместе с обычной видеорекламой, формат такой же, как у поля ad_events. 2021-06-25 — колонка удалена, Эфир закопан, а актуальна она была только для Эфира
#### shows_block_good (int64?)
Количество показанных рекламных блоков
#### shows_good (int64?)
Количество показанных рекламных роликов
#### sources_aggr (string)
Типы событий, которые присутствовали в сессии, через запятую. 
#### stream_block (string?)
Идентификатор блока на сервисе, в котором сейчас идёт смотрение, присылаемый в поле stream_block. Есть не на всех сервисах.
#### tcpinfo_total_retrans (int64?)
Суммарное количество tcpinfo_total_retrans из strm-access-log
#### test_buckets (string?)
Объединённые тестиды со всех сервисов. Там есть строковые тестиды Дзена, поэтому поле довольно большие, отфильтровать их можно так:
```
$getNonZenTestids = ($tb) -> {
    $sp1 = String::SplitToList($tb, ";");
    $testids = ListMap(
        $sp1, ($x)->(unwrap(String::SplitToList($x, ",")[0]))
    );
    $testids = ListFilter(
        $testids, ($x)->(cast($x as Int64) is not null)
    );
    return $testids
};

select $getNonZenTestids(test_buckets)
```
#### times_on_seekbar (any?)
Уникальные значения положения seekbar из логов, можно использовать для менее грубого, чем тупо по view_time, расчёта глубины просмотра (но пока этого никто не делал)
#### timestamp (int64?)
UNIX timestamp времени начала сессии в секундах
#### timetuple (any?)
Если это эфирная программа — то время её начала и конца
#### user_age_6s (any?)
Аналогично age_segments, но 6 категорий, а не 5
#### user_agent (string?)
Юзерагент
#### user_id (string?)
deprecated поле, не надо в него смотреть. Но наверное будет осмысленно положить туад 
#### user_license (string?)
Лицензия пользователя (Svod-пользователь может смотреть Svod-контент, а без лицензии он недоступен)
#### UUID (string?)
Чуть нормализованный идентификатор контента: для ВХ-базы — собственно UUID, 32-символьный `[0-9a-f]` идентификатор, начинающийся с `4`. Для новой UGC-базы — ≈10-символьная строчка, начинающаяся с `v`.
#### video_content_id (string?)
Идентификатор контента в том виде, какой он был в логах
#### view_time (int64?)
Время просмотра в секундах. Считается хитро и местами костыльно — если был хоть один хартбит, то минимальное из значений времени просмотра, посчитанных по хартбитам в gogol и redir-логе (допустим, в gogol 5 30-секундных хартбитов, а в redir 6 — view_time будет 150). Но если есть хартбиты только из одного лога, то view_time будет не 0, а значение по этому одному логу. Если ни одного хартбита не было, то берётся время по чанкам (таймстемп загрузки последнего чанка минус таймстемп загрузки первого), если оно меньше 10. Если оно больше 10, то 0.
#### view_time_non_muted (int64?)
Время просмотра со звуком, считается только по хартбитам
#### view_time_player_alive (double?)
Время просмотра по событиям PlayerAlive. По идее оно должно быть точнее, чем view_time, и без костылей, но PlayerAlive есть только в новых версиях плеера.
#### view_time_player_alive_non_muted (double?)
Время просмотра со звуком по событиям PlayerAlive
#### view_time_player_alive_visible_non_muted (double?)
Время просмотра со звуком и во вьюпорте по событиям PlayerAlive
#### view_type (string)
Тип просмотра — live, catchup или vod, посчитанный по heur_category и timetuple
#### vsid (string?)
64-символьный идентификатор плеера. Иногда в поле vsid будет строчка, начинающаяся с rtb% — это значит, что это не видеосмотрение, а видеореклама, в запросах за которой не был указан vsid, поэтому я не смог её приклеить к настоящей сессии смотрения, но чтобы не терять деньги, эти строчки остаются в кубах
#### winhits_block_good (int64?)
Количество блоков с винхитами
#### winhits_good (int64?)
Количество 
#### yandexuid (string?)
Кука yandexuid
#### yu_hash (string?)
Когда-то в далёкой галактике у нас был плеер первого канала, которому нельзя было отдавать наши яндексуиды, поэтому мы отдавали им хеши, соответственно по этому полю считалась аудитория. Сейчас оно не очень-то нужно, но сохранено во имя обратной совместимости