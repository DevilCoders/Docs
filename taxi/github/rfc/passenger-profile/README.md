# Сервис персонального профиля пассажира
Это чуть изменённый и дополненный RFC Кирилла (taxi/rfc#70), из которого убраны персональные предпочтения и добавлено фото пользователя.  

## Продуктовое описание
Сервис нужен для отображения персональных данных пассажира. На данный момент у сервиса предполагается три применения:

1. Отображение рейтинга пользователя
    -  Рейтинг раз в сутки (или чаще, если нужно) загружается из аналитической таблицы в YT
2. Отображение имени пользователя
    -  Во время поездки пользователю будет предложено сохранить свое имя, чтобы водители в будущем могли обращаться к пассажиру по имени (предлагается ограничить длину имени 100 символами)
    - По дефолту имя будет подтягиваться из паспорта (если аккаунт портальный)
    - Имя можно будет изменить в настройках профиля в меню
    - Имя не будет специально валидироваться на корректность
    - Имя нужно пробрасывать в таксометр, чтобы оно отображалось у водителя
3. Хранение фотографии пользователя
    - Пользователь сможет загрузить фотографию в профиль
    - Ссылка на фотографию пользователя будет прокидываться в таксометр вместе с именем
    - Пока что фотография не будет модерироваться

## Храние профиля пользователя
Для хранения профиля пользователя будет создан сервис `passenger-profile` на py3 с данными в постгресе.

В базе будет единственная таблица:
```sql
CREATE TYPE IF NOT EXISTS yandex_uid_type AS ENUM ('portal', 'phonish')

CREATE SCHEMA IF NOT EXISTS passenger_profile;
CREATE TABLE IF NOT EXISTS passenger_profile.profile (
    yandex_uid VARCHAR PRIMARY KEY,
    yandex_uid_type yandex_uid_type,
    application VARCHAR,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

### Разделение профиля по приложениям  

Чтобы пользователю убера не прилетал его рейтинг из яндекс-такси, профили будут храниться с учётом приложения (поле `application`).  
Будет создан новый конфиг `APPLICATION_MAP_PASSENGER_PROFILE`, в котором будет храниться маппинг возможных значений конфига `ALL_APPLICATIONS` на список приложений:
- yandex
- uber
- uber_kz
- uber_by
- uber_az
- yango
- ...


## Хранение имени пользователя

Нас интересует только имя пользователя (без фамилии), чтобы знать, как к нему обращаться. 
Имя без фамилии не является персональными данными. 
(см. https://st.yandex-team.ru/TAXIDWH-3512#5d3aad8d29af1d001ec76d2a)

```sql
ALTER TABLE passenger_profile.profile ADD COLUMN first_name VARCHAR NOT NULL DEFAULT "",  -- как обращаться к пользователю
```

### Имя по дефолту
Для портальных пользователей имя будет браться из Паспорта, если оно проходит проверку корректности.  
Для фонишей, привязанных к портальному аккаунту имя будет браться из привязанног портального аккаунта или из Паспорта.  
Если пользователь поменяет имя, оно не будет загружаться из связанных аккаунтов или из Паспорта.  
API Паспорта: https://doc.yandex-team.ru/blackbox/reference/method-userinfo-response-json.html  


### API
#### Изменение имени
Авторизация: passenger-authorizer  
RPS: пока не понятно, но вряд ли больше 200 RPS  

```http
PATCH /4.0/passenger-profile/v1/profile/

{
    "first_name": "name"
}
```
UID пользователя будет браться из хедера `X-Yandex-UID`
Связанные UID будут браться из хедера `X-Yandex-Bound-Uids`  
Оба хедера берутся из passenger-authorizer (см. https://wiki.yandex-team.ru/taxi/backend/architecture/passenger-authorizer/)

#### Получение имени
Есть два варианта:
##### Получить имя из ручки профиля
Авторизация: passenger-authorizer  
RPS: аналогично `/launch`
```http
GET /4.0/passenger-profile/v1/profile/
```
```json
{
    "passenger_profile": {
        "first_name": "name"
    }
}
```
Если у пользователя не задано имя, в поле `first_name` придёт пустая строка.

##### Получить имя в `/3.0/launch`
```
POST /3.0/launch
...
```
```json
{
    ...
    "passenger_profile": {
        "first_name": "name"
    }
    ...
}
```
Для этого можно сделать отдельную внутреннюю ручку с авторизацией через TVM
```http
GET /internal/passenger-profile/v1/profile/?yandex_uid=1235678?yandex_bound_uids=455678,456765
```
```json
{
    "passenger_profile": {
        "first_name": "name"
    }
}
```

###  Taximeter API
TODO: обсудить с командой таксометра

## Отображение рейтинга пользователя
Рейтинг пользователей будет лежать в таблице YT, откуда раз в сутки крон-таск будет копировать изменившиеся рейтинги в постгрес.

```sql
ALTER TABLE passenger_profile.profile ADD COLUMN rating VARCHAR;
```

В ручки `GET internal/passenger-profile/v1/profile/` и `GET 4.0/passenger-profile/v1/profile/` будет добавлено поле `rating`
```json
{
    "first_name": "Алексей",
    "rating": "4.9"
}
```

## Фотографии пользователей
У пользователя может быть только одна фотография. История не сохраняется.  
Хранение фотографии пользователя аналогично хранению фотографии водителя:
В Аватарницу MDS сохраняется три картинки: оригинал фотографии, ресайзнутая до 1080 пикселей в ширину фотография и аватарка — обрезанная по лицу фотография.
Если на картинке нет лица, фотография обрезается и ресайзится до размера аватарки.

Чтобы уменьшить размер отправляемого по сети файла, можно ресайзить фотографию на клиенте.  
Также предлагается обрезать аватарку тоже на клиенте, как это делает большинство сервисов (телеграм, твиттер, вк etc.)
Тогда вместе с фотографией клиент будет присылать координаты кропа аватарки,
а сервис будет по ним кропать и сохранять в mds.

### Хранение фотографий
Фотографии хранятся в MDS, в локальной базе хранятся ссылки на оригинал, ресайзнутую фотку и аватарку.
```sql
CREATE TABLE IF NOT EXISTS passenger_profile.photo (
    profile_uid VARCHAR REFERENCES profile,
    source_photo_url VARCHAR,
    full_size_url VARCHAR,
    avatar_url VARCHAR,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```
### API
#### Сохранение фотографии
```http
PUT /4.0/passenger-profile/v1/profile/photo
Content-Type: multipart/form-data
```
```json
{
    "full_size_url": "https://avatars.mdst.yandex.net/...",
    "avatar_url": "https://avatars.mdst.yandex.net/..."
}
```
Возможные ошибки:
    - фотография слишком большая (> 20мб)
    - фотография слишком маленькая (< 200px по обоим измерениям)
    - фотография не в jpeg
    - ошибка загрузки. в этом случае клиенту стоит попытаться повторить загрузку
    - невалидные координаты кропа

### Получение фотографии
Ссылки на фотографию профиля будут приходить в ручке запроса профиля и в /launch:
```http
GET /4.0/passenger-profile/v1/profile
```
```json
{
    "rating": "4.9",
    "first_name": "Алексей",
    "photo":
        {
            "full_size_url": "https://avatars.mdst.yandex.net/...",
            "avatar_url": "https://avatars.mdst.yandex.net/..."
        }
}
```

### Takeout API
Необходимо будет интегрироваться с [Takeout API](https://wiki.yandex-team.ru/users/e-usov/taxi-takeout/) 
