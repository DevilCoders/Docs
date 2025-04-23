# Settings page

This repo contains implementation of our settings pages: desktop and mobile.

## Setup

```sh
nvm use && npm i
```

## Development

```sh
npm run dev:desktop
npm run dev:mobile
```

## Build

```sh
npm run build:desktop
npm run build:mobile
```

## API

- **Endpoint:** `https://sovetnik.market.yandex.ru/settings`
- **Content-type:** `json`

### Initial response

| Description                                     | Method |
| ----------------------------------------------- | ------ |
| С автоопределением региона и без списка доменов | `GET`  |

**Response:**

```json
{
  "autoShowShopList": true,
  "activeCity": {},
  "activeCountry": {},
  "otherRegions": true,
  "disabledDomains": [],
  "sovetnikRemoved": null,
  "canRemoveSovetnik": false,
  "showProductNotifications": true,
  "showAviaNotifications": true,
  "showAutoNotifications": true
}
```

| Description                            | Method |
| -------------------------------------- | ------ |
| С указанным регионом и списком доменов | `GET`  |

**Response:**

```json
{
  "autoShowShopList": true,
  "activeCity": {
    "id": 213,
    "name": "Москва"
  },
  "activeCountry": {
    "id": 225,
    "name": "Россия"
  },
  "otherRegions": true,
  "disabledDomains": ["example1.com", "example2.com"],
  "sovetnikRemoved": null,
  "canRemoveSovetnik": false,
  "showProductNotifications": true,
  "showAviaNotifications": true,
  "showAutoNotifications": true
}
```

### Set region automatically

| Description                     | Method |
| ------------------------------- | ------ |
| Определять регион автоматически | `POST` |

**Payload:**

```json
{
  "settings": {
    "typeRegion": "regionAutoDetect",
    "activeCountry": {},
    "activeCity": {}
  }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": {
    "typeRegion": "regionAutoDetect",
    "activeCountry": {},
    "activeCity": {}
  }
}
```

### Set region manually

| Description            | Method |
| ---------------------- | ------ |
| Указать регион вручную | `POST` |

**Payload:**

```json
{
  "settings": {
    "activeCity": {
      "id": 213,
      "name": "Москва"
    },
    "activeCountry": {
      "id": 225,
      "name": "Россия"
    }
  }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": {
    "activeCity": {
      "id": 213,
      "name": "Москва"
    },
    "activeCountry": {
      "id": 225,
      "name": "Россия"
    }
  }
}
```

### Show offers from other regions

| Description                               | Method |
| ----------------------------------------- | ------ |
| Показывать предложения из других регионов | `POST` |

**Payload (on):**

```json
{
  "settings": { "otherRegions": true }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": {
    "otherRegions": true
  }
}
```

**Payload (off):**

```json
{
  "settings": { "otherRegions": false }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": {
    "otherRegions": false
  }
}
```

### Show popup on hover

| Description                                    | Method |
| ---------------------------------------------- | ------ |
| Показывать список при наведении указателя мыши | `POST` |

**Payload (on):**

```json
{
  "settings": { "autoShowShopList": true }
}
```

**Response:**
```json
{
  "ok": true,
  "settings": { "autoShowShopList": true }
}
```

**Payload (off):**

```json
{
  "settings": { "autoShowShopList": false }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": { "autoShowShopList": false }
}
```

### Allow product notifications

| Description                                  | Method |
| -------------------------------------------- | ------ |
| Уведомлять меня о предложениях цен и похожих товаров | `POST` |

**Payload (on):**

```json
{
  "settings": { "showProductNotifications": true }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": { "showProductNotifications": true }
}
```

**Payload (off):**

```json
{
  "settings": { "showProductNotifications": false }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": { "showProductNotifications": false }
}
```

### Allow avia notifications

| Description                                      | Method |
| ------------------------------------------------ | ------ |
| Уведомлять меня о предложениях цен на авиабилеты | `POST` |

**Payload (on):**

```json
{
  "settings": { "showAviaNotifications": true }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": { "showAviaNotifications": true }
}
```

**Payload (off):**

```json
{
  "settings": { "showAviaNotifications": false }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": { "showAviaNotifications": false }
}
```

### Allow auto notifications

| Description                                      | Method |
| ------------------------------------------------ | ------ |
| Уведомлять меня о предложениях похожих автомобилей | `POST` |

**Payload (on):**

```json
{
  "settings": { "showAutoNotifications": true }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": { "showAutoNotifications": true }
}
```

**Payload (off):**

```json
{
  "settings": { "showAutoNotifications": false }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": { "showAutoNotifications": false }
}
```

### Add domain to blacklist

| Description                                                        | Method |
| ------------------------------------------------------------------ | ------ |
| Добавить домен в список сайтов, где Советник не должен срабатывать | `POST` |

**Payload:**

```json
{
  "settings": {
    "disabledDomains": [
      {
        "type": "add",
        "domain": "example.com"
      }
    ]
  }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": {
    "disabledDomains": [
      "example.com"
    ]
  }
}
```

### Remove domain from blacklist

| Description                                                        | Method |
| ------------------------------------------------------------------ | ------ |
| Удалить домен из списка сайтов, где Советник не должен срабатывать | `POST` |

**Payload:**

```json
{
  "settings": {
    "disabledDomains": [
      {
        "type": "remove",
        "domain": "example.com"
      }
    ]
  }
}
```

**Response:**

```json
{
  "ok": true,
  "settings": {
    "disabledDomains": []
  }
}
```
