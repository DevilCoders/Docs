# Быстрый старт

Код Фронтенд пользовательской части [Яндекс.Маркета](https://market.yandex.ru) хранится [в Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/marketfront).

## Структура проекта

**Цель** — максимально выносить код в `src` и переиспользовать.

Сейчас проект представляет из себя древнерусского мифологического дракона
- `market`. Непосредственно, код фронтенда [Яндекс.Маркета](https://market.yandex.ru)
- `api`. Непосредственно, код FAPI
- `pokupki`. Остатки кода фронта Беру, он не собирается и практически не используется, скоро будет удален.

### F.A.Q

- Q: Как создать проект на Логрусе?
- A: Чтобы развернуть код на Логрусах, нужно выполнить команду `make_wc`

## Подготовка к работе

- Проекту нужна `node 16.9.1`, `npm 6.13` и [veendor](https://www.npmjs.com/package/veendor) локально;
- Разрабатывать придется на "логрусе". Подробнее об этом написано в [руководстве новичка](https://wiki.yandex-team.ru/market/frontend/dev-environment/) на вики;

```bash
nvm install 16.9.1 && nvm alias default 16.9.1 && npm i -g veendor && npm i -g npm@^6.13
```

## Полезные ссылки

- [Общие соглашения](https://wiki.yandex-team.ru/market/frontend/conventions)
- [Документация](https://wiki.yandex-team.ru/market/frontend/dev-environment/)
- [Очередь в Трекере](https://st.yandex-team.ru/MARKETFRONT)
- [Пайплайны](https://tsum.yandex-team.ru/pipe/projects/front-market-unified)
- [FAPI документация](https://marketfront.s3.mds.yandex.net/arcadia-ci/fapi-docs/index.html)
- [Levitan 2.0 develop](https://levitan.yandex-team.ru/market/develop/sandbox?code=DwGQhgXgngSgpgOwCZwE4D5Am5AbzAZygQGMACAMwFdiAXASwHsEAKAShO0xK5KMb2vYAJOGCS0EAcwC%2BJALwkwAdzC0BqOHnoAbAG5wmAcgACUMMjgAPALRa4O1WYD0AIwBMzgywDcnbuuoUqAgkrHLoIb7c3MBYUXHRwqLiEiR4tBBwstgAjDKKcLQSABbUsgBEztpIZbHxdVzCWlr0JADq9KhaSACEkfUkwI6JYpK18YNjJN6YUlKYg%2BDQ8OYYQA)
