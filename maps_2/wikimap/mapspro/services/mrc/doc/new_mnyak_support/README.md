В новой версии мобильного приложения Народная карта предполагается развить сценарии пользователя в работе с поездками и сообщениями о неточности:
- ведение съемки в экономичном режиме (при этом снимки должны делаться только там, где текущее покрытие устарело);
- просматривание единым списком информацию о всех поездках (сообщениях о неточностях), выгруженных и невыгруженных;
- узнавание о дополнительной пользе от собранных фотографий, в частности о количестве сгенерированных гипотез.

Здесь описаны предложения по реализации новых сценариев пользователя Мобильной Народной карты с точки зрения клиент-серверных протоколов.

### Показ объединенного списка поездок

В приложении нужно будет показывать список всех поездок пользователя, выгруженных и невыгруженных, по каждой поездке будет необходимо отображать:
- время начала поездки
- суммарное количество фотографий
- продолжительность поездки
- длина маршрута поездки
- объем данных для выгрузки
- изображение с превью поездки
- статус: ожидает выгрузки, выгружается, на проверке, обработан
- кол-во сгенерированных предположений

#### Как реализовано сейчас

##### На стороне мобильной библиотеки

При создании поездки ее идентификатор `ride_id` [генерируется](https://a.yandex-team.ru/arc_vcs/maps/mobile/libs/mrc/common/utils/common.cpp?rev=r9050013#L99) в виде `uptime_ms + random_string`.

Для каждой поездки по идентификатору `ride_id` в постоянную память сохраняются время начала, общая длительность поездки, а также фотографии и GPS-трек.

Однако на сервер выгружатся лишь снимки и треки, без привязки к поездкам.

```(c++)
message TrackPoint
{
    required uint64 time = 1; // milliseconds since epoch
    required Location location = 2;
}

message Image {
    required uint64 created = 1; // milliseconds since epoch
    required bytes image = 2;
    optional Location estimatedPosition = 3;
}


message Results {
    enum Id { ID = 50000; }
    repeated Image images = 1;
    repeated TrackPoint track = 2;
    repeated bytes reports = 3;
    // ...
}
```

Для каждой поездки в мета-базе сейчас сохраняются:
- время начала поездки
- общая продолжительность

##### На серверной стороне

Процесс [ride_manager](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/utility.h?rev=r8989647#L41) анализирует поток выгружаемых фотографий, группирует фотографии в поездки по идентификатору источника `source_id` и времени съемки. В результате его работы наполняется таблица `ride.ride`

| Column                   | Type                      | Nullable |
|--------------------------|---------------------------|----------|
| ride_id                  | bigint                    | not null |
| user_id                  | text                      | not null |
| start_time               | timestamp with time zone  | not null |
| end_time                 | timestamp with time zone  | not null |
| source_id                | text                      | not null |
| track                    | geometry(LineString,3395) | not null |
| distance_in_meters       | double precision          | not null |
| photos                   | bigint                    | not null |
| upload_start_time        | timestamp with time zone  | not null |
| upload_end_time          | timestamp with time zone  | not null |
| is_deleted               | boolean                   | not null |
| show_authorship          | boolean                   |          |
| status                   | enum                      |          |

Изменения из таблицы `ride.ride`  затем копируются процессом [ugc_uploader](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ugc_uploader) в сервис [maps-core-ugc-account](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/account), хранящий "вклады" пользователей в развитие сервисов Гео.

Каждая поездка пользователя превращается во "вклад" следующего [формата](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/contributions/mrc_ride.proto?rev=r8690957#L9):
```
message RideContribution {
    required string id = 1;
    optional common2.i18n.Time started_at = 2;
    optional common2.i18n.Time finished_at = 3;
    optional common2.i18n.LocalizedValue duration = 4;
    optional common2.i18n.LocalizedValue distance = 5;
    optional uint32 photos_count = 6;
    optional common2.Image album_image = 7;

    message RideStatus {
        message Pending {}
        message Processed {}

        oneof status {
            Pending pending = 1;
            Processed processed = 2;
        }
    }

    optional RideStatus ride_status = 8;
    optional bool show_authorship = 9;
}
```

#### Объединение данных по поездкам в мобильной библиотеке

Для каждой поездки потребуется вычислять и хранить в мета-базе:
- длину поездки
- общее количество созданных снимков

Чтобы показывать объединенный список из невыгруженных и выгруженных поездок нам потребуется уметь мерджить данные о поездках, хранимые локально с данными, доступными на сервере.

Чтобы это стало возможным, необходимо при выгрузке изображений и треков из мобильной библиотеки на сервер передавать также `ride_id`, уникально идентифицирующий поездку на устройстве.

```
message Results {
    enum Id { ID = 50000; }
    repeated Image images = 1;
    repeated TrackPoint track = 2;
    repeated bytes reports = 3;
    // ...
    optional string client_ride_id = 10;
}
```

Для получения в мобильной библиотеке информации о поездках пользователя наиболее логичным вариантом видится использование текущего [API maps-core-nmaps-ugc-account](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Api.md#/v1/contributions/find), в частности ручки `GET /v1/contributions/find`. Соответствущий конфиг в мобильной прокси может выглядеть следующим образом:

```
location /mrc/ugc_account/2.x/contributions/find {
    access_by_lua_file /usr/lib/yandex/maps/rate-limiter/access.lua;

    proxy_set_header Accept application/x-protobuf;
    proxy_set_header Host $ugc_account_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Yandex-Http2 $http2;
    proxy_set_header X-Yandex-Ja3 $http_ssl_ja3;
    proxy_set_header X-Forwarded-For-Y $remote_addr;
    proxy_set_header X-Source-Port-Y $remote_port;
    proxy_set_header Accept-Encoding $http_accept_encoding;

    set $access 'yandex_only';
    set $access_user_ticket 'True';
    set $tvm_dst 'maps-core-ugc-account';

    set_by_lua_file $args /usr/lib/yandex/maps/mobile/urlparams_filter.lua
        lang metadata_ids base_id before_limit after_limit;

    proxy_pass http://ugc_account_upstream/v1/contributions/find;
}

```

В `RideContribution` необходимо добавить генерируемый на клиенте идентификатор поездки, а также информацию о сгенерированных гипотезах.

```
message RideContribution {
    required string id = 1;
    optional common2.i18n.Time started_at = 2;
    optional common2.i18n.Time finished_at = 3;
    optional common2.i18n.LocalizedValue duration = 4;
    optional common2.i18n.LocalizedValue distance = 5;
    optional uint32 photos_count = 6;
    optional common2.Image album_image = 7;

    message RideStatus {
        message Pending {}
        message Processed {}

        oneof status {
            Pending pending = 1;
            Processed processed = 2;
        }
    }

    optional RideStatus ride_status = 8;
    optional bool show_authorship = 9;

    optional string client_ride_id = 10;

    message HypothesesInfo {
        optional uint32 count = 1;
    }

    optional HypothesesInfo hypotheses = 11;
}
```

Желаемое поведение при возможных сочетаниях состояний хранения данных на клиенте и сервере описаны в таблице:

| На стороне клиента | На стороне сервера | Поведение |
|--------------------------|---------------------------|----------|
| метаинформация с всеми фотографиями и треком | отсутствует | использовать локальные данные |
| метаинформация с частью фотографий и трека | фотографии и трек получены, но RideContribution еще не сформирован | использовать локальные данные |
| метаинформация с частью фотографий и трека | фотографии и трек получены, RideContribution сформирован | использовать локальные данные |
| только метаинформация | фотографии и трек получены, но RideContribution еще не сформирован | использовать локальные данные |
| только метаинформация | фотографии и трек получены, RideContribution сформирован | использовать данные из RideContribution, метаинформацию удалить |
| отсутствует | фотографии и трек получены, RideContribution сформирован | использовать данные из RideContribution |


#### Изменения в idl

Идея разбивается о реальность, для локальных и серверных поездок сложно предоставить единый интерфейс доступа:
1) про изменение состояния локальных поездок необходимо уведомлять клиента, в настоящее время подпись на изменения поездки осуществляется в самом объекте Ride, а он предоставляется в клиента по `weak_ref`
2) применение этого же подхода для отображения серверных поездок будет очень дорогим: библиотеке придется постоянно загружать всю информацию по всем поездкам, это создаст лишние накладные расходы и противоречит принципу “don't pay for what you don't use”

Исходя из этих соображений следует, что если и будет унифицированный интерфейс получения информации по поездкам, то он будет иметь иной вид: это скорее должен быть постраничный фид поездок, аналогичный [фиду дорожных событий](https://a.yandex-team.ru/arc_vcs/maps/mobile/libs/mapkit/road_events/idl/mapkit/road_events/road_events_manager.idl)

```
struct RideInfo {
    enum Status {
        ReadyForUpload,
        Uploading,
        ProcessingOnServer,
        Processed
    }

    string id;
    Status status;
    optional abs_timestamp started;
    optional abs_timestamp finished;
    int64 totalPhotosCount;
    mapkit.LocalizedValue duration;
    runtime.Error storageError readonly;
}

interface RidesFeedSession {
    lambda listener FeedListener (objc:ResponseHandler) {
        void onFeedReceived(const vector<RideInfo> rides);
        void onFeedError(runtime.Error error);
    }

    bool hasNextPage() const;
    /**
     * One of the following errors can occur: {@link runtime.network.NotFoundError},
     * {@link runtime.network.NetworkError}, {@link runtime.network.RemoteError}.
     */
    void fetchNextPage(FeedListener feedListener);

    void cancel();
}

weak_ref interface RideManager {

	  lambda listener RideListener(objc:RideUpdateHandler) {
	      void onRideChanged(RideInfo ride);
    }

    RidesFeedSession rides(uint pageSize);
}
```

Однако в этом случае возникает сложность в отображении поездок в условиях отсутсвия Интернета. С точки зрения приложения естественно ожидать, что информация о локальных поездках доступна всегда, безотносительно доступности сети.

Следовательно, интерфейсы доступа к локальным и серверным поездкам должны быть разделены.

### Редактирование поездки

У пользователя должна быть возможность просматривать список фотографий поездки, управлять показом логина на них, а также удалять подмножества фотографий с концов поездки.

*ВАЖНО* Здесь мы предполагаем, что клиент выгружает снимки на сервер в хронологическом порядке, это значит, что все локально хранимые на клиенте снимки сняты позже тех, что хранятся на сервере.

#### Текущая реализация

В настоящее время сервис `maps-core-nmaps-mrc-ugc-back` предоставляет доступ к фотографиям и треку поездки, управлять видимостью логина, а также позволяет удалять части фотографий с концов.

[Api сервиса](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcugc/README.md?blame=true) включает следующие ручки:
- `GET /v1/rides/my/get` -- для получения обзорной информации по поездке
- `POST /v1/rides/my/chunk` -- для получения данных фотографий для фрагмента поездки
- `GET /v1/rides/my/photo` -- получение изображения конкретной фотографии
- `PUT /v1/rides/my/update` -- управление видимостью логина и удаление фотографий с концов поездки
- `DELETE /v1/rides/my/delete` -- удаление всей поездки целиком

Реализации показа фотографий поездки и редактирования поездки на клиенте потребуется добавить знание про эти ручки в мобильную прокси:

```
location /mrc/ugc_back/2.x/rides/get {
    set_by_lua_file $args /usr/lib/yandex/maps/mobile/urlparams_filter.lua
        lang ride_id;

    proxy_pass http://ugc_back_upstream/v1/rides/my/get;
}

location /mrc/ugc_back/2.x/rides/chunk {
    proxy_pass http://ugc_back_upstream/v1/rides/my/chunk;
}

location /mrc/ugc_back/2.x/rides/photo {
    set_by_lua_file $args /usr/lib/yandex/maps/mobile/urlparams_filter.lua
        lang id;

    proxy_pass http://ugc_back_upstream/v1/rides/my/photo;
}

location /mrc/ugc_back/2.x/rides/update {
    set_by_lua_file $args /usr/lib/yandex/maps/mobile/urlparams_filter.lua
        lang ride_id;

    proxy_pass http://ugc_back_upstream/v1/rides/my/update;
}

location /mrc/ugc_back/2.x/rides/delete {
    set_by_lua_file $args /usr/lib/yandex/maps/mobile/urlparams_filter.lua
        ride_id;

    proxy_pass http://ugc_back_upstream/v1/rides/my/delete;
}
```


#### Показ галереи фотографий поездки

Желаемое поведение при возможных сочетаниях состояний хранения данных на клиенте и сервере описаны в таблице:

| На стороне клиента | На стороне сервера | Поведение |
|--------------------------|---------------------------|----------|
| метаинформация с всеми фотографиями и треком | отсутствует | использовать локальные данные |
| метаинформация с частью фотографий и трека | фотографии и трек получены, но RideContribution еще не сформирован | общее количество фотографий достоверно известно по метаинформации, в галерее снимков отображать изображения локально хранимых изображений, для остальных показывать специальный статус "изображение недоступно" |
| метаинформация с частью фотографий и трека | фотографии и трек получены, RideContribution сформирован | общее количество фотографий достоверно известно по метаинформации, в галерее снимков отображать объединение локального множества снимков и снимков, доступных с сервера |
| только метаинформация | фотографии и трек получены, но RideContribution еще не сформирован | отображать галерею, в которой все снимки  имеют статус "изображение недоступно"|
| только метаинформация | фотографии и трек получены, RideContribution сформирован | использовать данные из RideContribution|
| отсутствует | фотографии и трек получены, RideContribution сформирован | -//- |

#### Удаление фотографий с концов поездки

У пользователя должна быть возможность удалить все фотографии, находящиеся до (или после) заданной. Удаление доступно только для локально хранимых снимков и для снимков, которые уже учтены в RideContribution и доступны из сервиса `maps-core-nmaps-mrc-ugc-back`.
