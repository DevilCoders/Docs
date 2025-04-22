# I-UA

## Установка

```bash
npm i -S @yandex-lego/i-ua --registry https://npm.yandex-team.ru
```

## Использование

При импорте модуля, на `HTML` устанавливаются классы-хелперы.
```js
import '@yandex-lego/i-ua'
import { ios, iphone } from '@yandex-lego/i-ua'
```

## API

* **ie** — возвращает версию Internet Explorer
* **ios** — возвращает версию iOS
* **android** — возвращает версию Android
* **wp** — возвращает версию Windows Phone
* **iphone** — проверяет, является ли устройство iphone
* **ipad** — проверяет, является ли устройство ipad
* **server** — проверяет, выполняется ли код на сервере

## Список поддерживаемых классов

* `i-ua_orient_[landscape|portrait]`
* `i-ua_platform_[ios|android|wp|other]`
* `i-ua_retina_yes`
* `i-ua_svg_[yes|no]`
* `i-ua_inlinesvg_[yes|no]`
* `i-ua_object-fit_no`
