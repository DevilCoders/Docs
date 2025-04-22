# Adfox - баннерная система на маркете

## Структура стейта

`Adfox.data.collections.banners` -- коллекция баннеров по ключу, идентично раскодированному из base64 значению `content`
баннера у adfox.
Ключем является вызов функции `generateKeyByBannerParams` от параметров __запроса__ баннеров (`id` и `p2`)

# Ручки

## Получить баннеры балково

## POST /<clientId>/getBulk/v1

Поддержаны параметры: `id`, `p2` по комбинации которых выбирается баннер

Описание известных параметров можно посмотреть
[тут](https://wiki.yandex-team.ru/adfox/support/Znachenijaparametrovzaprosavkodevstavki/)

# Хелперы

## generateAdfoxBanner
Генерирует объект баннера после раскодировки из base64

## generateKeyByBannerParams
Генерирует ключ для хранения баннера в коллекции на основе id (ad_place) и p2 (type)
