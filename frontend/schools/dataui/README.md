## DATAUI

Предназначена для разработки инфраструктурных, внутренних и облачных сервисов.

Текущие пользователи: Яндекс.Облако (консоль, бэкофис, партнёрский портал), Datalens, YT, Logbroker, Внутреннее облако (infracloud), ABT, Мониторинг и другие.

|||
| -------- | ------ |
| Дизайн система | [Common](https://cloud-guide.yandex-team.ru) |
| Документация | [ui.yandex-team.ru](https://ui.yandex-team.ru) |
| Трекер | [DATAUI](https://st.yandex-team.ru/DATAUI) |
| Компоненты| [Common](https://github.yandex-team.ru/data-ui/common) |

### Фронтенд технологии

|||
| -------- | ------ |
| Язык | TypeScript / JavaScript |
| Шаблоны | React |
| Стейт | Redux |
| CSS | SCSS |
| Сборка | ~~Webpack~~ [UI Core](https://github.yandex-team.ru/data-ui/ui-core) |
| Nodejs | ~~Express~~ [Core](https://github.yandex-team.ru/data-ui/core) |
| SQL | [Core DB](https://github.yandex-team.ru/data-ui/core-db) |
| Линтеры| [dataui eslint](https://github.yandex-team.ru/data-ui/eslint-config) |
| Пакетный менеджер | NPM ||
| i18n | [dataui i18n](https://github.yandex-team.ru/data-ui/i18n) |
| Unit| Jest||
| CI| [Farm](https://github.yandex-team.ru/data-ui/farm), TeamCity ||
| Deploy| Qloud, Deploy, Y.Cloud ||
| Авторизация| Blackbox (tvm), Y.Cloud (IAM, SAML) ||


## Быстрый старт

```
1. git clone git@github.yandex-team.ru:data-ui/ui-core-template.git
2. rm -rf .git && git init
3. Замените `app-name-placeholder` на имя вашего приложения в `package.json` и `src/index.ts`.
3. npm ci
4. npm run dev
```

Больше информации по настройке и эксплуатации доступно в нашей документации: https://ui.yandex-team.ru/

## Если есть вопросы

Приходите в чатик [DataUI Tech](https://t.me/joinchat/BpUNFE6mDwalY2r4_TRrZg), задавайте вопросы, помогайте делать общие технологии лучше.
