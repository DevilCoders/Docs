# Список сборок

## Мессенджер

<a href="https://jing.yandex-team.ru/files/joshuan/yamb.png" target="_blank"><img align="right" width="300" src="https://jing.yandex-team.ru/files/joshuan/yamb.png"></a>

### `/chat`, `/chat?build=yamb`

Используется для чатов Яндекс.Коннект

**Доступен с:** `yandex.{tld}`

**Конфиг Webpack:** [.config/webpack/yamb/web.js](/.config/webpack/yamb/web.js)

**Шаблон HTML:** [public/yamb.html](/public/yamb.html)

**Главная точка входа:** [src/client/entries/web.ts](/src/client/entries/web.ts)

**Тайпинг конфига:** [src/client/config/index.ts](src/client/config/index.ts)

**Конфиг:**
* [src/client/config](/src/client/config)
* [src/client/config/targets/web](src/client/config/targets/web)

**CSP:** [src/configs/csp/yamb.js](/.config/csp/build/yamb.js)


<a href="https://jing.yandex-team.ru/files/joshuan/yamb-internal.png" target="_blank"><img width="300" align="right" src="https://jing.yandex-team.ru/files/joshuan/yamb-internal.png"></a>

### `/chat?build=yamb-internal`


Используется для чатов [Q](https://q.yandex-team.ru)

**Доступен с:** `yandex-team.ru`

**Конфиг Webpack:** [.config/webpack/yamb/web-internal.js](/.config/webpack/yamb/web-internal.js)

**Шаблон HTML:** [public/yamb.html](/public/yamb.html)

**Главная точка входа:** [src/client/entries/web.ts](/src/client/entries/web.ts)

**Тайпинг конфига:** [src/client/config/index.ts](src/client/config/index.ts)

**Конфиг:**
* [src/client/config](/src/client/config)
* [src/client/config/internal](src/client/config/internal)
* [src/client/config/targets/web](src/client/config/targets/web)
* [src/client/config/targets/web/internal](src/client/config/targets/web/internal)

**CSP:** [src/configs/csp/yamb-internal.js](/.config/csp/build/yamb-internal.js)


<a href="https://jing.yandex-team.ru/files/joshuan/chamb.png" target="_blank"><img width="300" align="right" src="https://jing.yandex-team.ru/files/joshuan/chamb.png"></a>

### `/chat?build=chamb`

Используется для внешних сервисов Яндекс

**Доступен с:** `yandex.{tld}`

**Конфиг Webpack:** [config/webpack/chamb/static.js](/config/webpack/chamb/static.js)

**Шаблон HTML:** [public/chamb.html](/public/chamb.html)

**Главная точка входа:** [src/client/entries/chamb.ts](/src/client/entries/chamb.ts)

**Тайпинг конфига:** [src/client/config/index.ts](src/client/config/index.ts)

**Конфиг:**
* [src/client/config](/src/client/config)
* [src/client/config/targets/embed](src/client/config/targets/embed)

**CSP:** [src/configs/csp/chamb.js](/.config/csp/build/chamb.js)


<a href="https://jing.yandex-team.ru/files/joshuan/yamb-embed-internal.png" target="_blank"><img width="300" align="right" src="https://jing.yandex-team.ru/files/joshuan/yamb-internal-embed.png"></a>

### `/chat?build=embed-internal`

Используется для внутренних сервисов Яндекс

**Доступен с:** `yandex-team.ru`

**Конфиг Webpack:** [.config/webpack/yamb/embed.js](/.config/webpack/yamb/embed.js)

**Шаблон HTML:** [public/yamb.html](/public/yamb.html)

**Главная точка входа:** [src/client/entries/embed.ts](/src/client/entries/embed.ts)

**Тайпинг конфига:** [src/client/config/index.ts](src/client/config/index.ts)

**Конфиг:**
* [src/client/config](/src/client/config)
* [src/client/config/internal](src/client/config/internal)
* [src/client/config/targets/embed](src/client/config/targets/embed)

**CSP:** [src/configs/csp/yamb-embed-internal.js](/.config/csp/build/yamb-embed-internal.js)

<a href="https://jing.yandex-team.ru/files/joshuan/widget.png" target="_blank"><img width="300" align="right" src="https://jing.yandex-team.ru/files/joshuan/widget.png"></a>

### `/chat?build=widget`

Используется для внешних сайтов. Является виртуальным билдом widget, основанный на yamb

**Доступен с:** `yandex.{tld}`

**Конфиг:**
* [src/client/config](/src/client/config)
* [src/client/config/targets/widget](src/client/config/targets/widget)

**CSP:** [src/configs/csp/yamb-widget.js](/.config/csp/build/yamb-widget.js)


### `/chat?build=yabro`

Используется для Яндекс.Браузер

**Доступен с:** `yandex.{tld}`

**Конфиг Webpack:** [.config/webpack/yamb/yabro.js](/.config/webpack/yamb/yabro.js)

**Шаблон HTML:** [public/yabro.html](/public/yabro.html)

**Главная точка входа:** [src/client/entries/yabro.ts](/src/client/entries/yabro.ts)

**Тайпинг конфига:** [src/client/config/index.ts](src/client/config/index.ts)

**Конфиг:**
* [src/client/config](/src/client/config)
* [src/client/config/targets/web](src/client/config/targets/web)

**CSP:** [src/configs/csp/yabro.js](/.config/csp/build/yabro.js)


### Внешние приложения

Используется для Яндекс.Коннект

**Конфиг Webpack:** [.config/webpack/yamb/desktop.js](/.config/webpack/yamb/desktop.js)

**Шаблон HTML:** [public/desktop.html](/public/desktop.html)

**Главная точка входа:** [src/client/entries/desktop.js](/src/client/entries/desktop.js)

**Тайпинг конфига:** [src/client/config/index.ts](src/client/config/index.ts)

**Конфиг:**
* [src/client/config](/src/client/config)
* [src/client/config/targets/desktop](src/client/config/targets/desktop)


### Внутренние приложения

Используется для [Q](https://q.yandex-team.ru)

**Конфиг Webpack:** [.config/webpack/yamb/desktop-internal.js](/.config/webpack/yamb/desktop-internal.js)

**Шаблон HTML:** [public/desktop.html](/public/desktop.html)

**Главная точка входа:** [src/client/entries/desktop.js](/src/client/entries/desktop.js)

**Тайпинг конфига:** [src/client/config/index.ts](src/client/config/index.ts)

**Конфиг:**
* [src/client/config](/src/client/config)
* [src/client/config/internal](src/client/config/internal)
* [src/client/config/targets/desktop](src/client/config/targets/desktop)
* [src/client/config/targets/desktop/internal](src/client/config/targets/desktop/internal)

## Стенд iframe

### `/chat?build=iframe-stand`

**Конфиг Webpack:** [services/iframe-stand/.config/webpack.config.js](/src/stands/iframe/webpack.config.js)

**Шаблон HTML:** [services/iframe-stand/public/iframe-stand.html](/src/stands/iframe/iframe-stand.html)

**Главная точка входа:** [services/iframe-stand/src/index.tsx](/src/stands/iframe/index.tsx)
