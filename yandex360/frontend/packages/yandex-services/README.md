# yandex-services
Ссылки для сервисов Яндекса

## Установка
```
npm i --save yandex-services --registry=http://npm.yandex-team.ru
```

## Использование
```javascript

const services = require('yandex-services');

// Общий конфиг с ссылками
const urls = services.services;
// ссылки для yandex-team домена
const yaTeam = services['yandex-team'];

// функция фильтрации
const filter = services.filter;

const urlsByService = filter({ services: 'mail' });
const urlsByDomain = filter({ domains: 'ru' });
const urlsByServicesAndDomains = filter({ services: ['mail', 'disk'], domains: ['ru', 'ua'] });


// Подключение ссылок по доменам на прямую
const ruUrls = require('yandex-services/dist/domains/ru.json');
const uaUrls = require('yandex-services/dist/domains/ua.json');

// Подключение ссылок по сервисам
const mailUrls = require('yandex-services/dist/services/mail.json');
const diskUrls = require('yandex-services/dist/services/disk.json');
```

Собранная версия для клиента находится в `yandex-services/dist/bundle.js`, по возможности на клиенте стоит подключать подоменный или сервисный json-конфиг вместо `bundle.js`, так как с добавлением сервисов `bundle.js` будет увеличиваться в размере.
## Формат файлов конфигов

#### Общий файл конфигов ссылок
`yandex-services.json`
```json
{ 
  "mail": {
	"ru": {
		"url": "https://mail.yandex.ru"
	},
	"am": {
		"url": "https://mail.yandex.com.am"
	},
	"az": {
		"url": "https://mail.yandex.az"
	},
	
	...
  },
  ...
}
```

#### Файлы с ссылками по доменам
`yandex-services/dist/domains/ru.json`
```json
{
    ...
    "images": {
      "url": "https://yandex.ru/images/"
    },
    "mail": {
      "url": "https://mail.yandex.ru"
    },
    "maps": {
      "url": "https://maps.yandex.ru"
    },
    "market": {
      "url": "https://market.yandex.ru"
    },
    ...
}

```

#### Файлы с ссылками по сервисам
`yandex-services/dist/services/mail.json`
```json
{
    ...
    "il": {
        "url": "https://mail.yandex.co.il"
    },
    "kg": {
        "url": "https://mail.yandex.kg"
    },
    "kz": {
        "url": "https://mail.yandex.kz"
    },
    "lt": {
        "url": "https://mail.yandex.lt"
    },
    "lv": {
        "url": "https://mail.yandex.lv"
    },
   ...
}   
```

