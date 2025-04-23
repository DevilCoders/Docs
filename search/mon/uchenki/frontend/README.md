# UI Ученек

![](https://jing.yandex-team.ru/files/alexunix/uchenkiui.png)
Подробнее -> [«Ученьки»](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/uchenki/)

UI cделан на [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app)

[React](https://reactjs.org) - ну, а что ещё, только функциональные компоненты, хуки (> 16.8.0).  
[Recoil](https://recoiljs.org) - глобальный стейт приложения.  
[useSWR](https://swr.vercel.app) - хук для кэширования, ретрая, инвалидации запросов, всего, что связано с запросами в API.  
[Next.js](https://nextjs.org) - роутинг, структурирование кода, рендеринг на сервере.  
[React-Bootstrap](https://react-bootstrap.github.io) - «UI Kit» т.е. замена Лего.  
[Ramba](https://ramdajs.com) - либа для функциональной парадигмы программирования, там где недостаточно магии ES6.

## Разработка

Необходимо отредактировать урл бэкэнда (либо на локальный, либо на престейбл) по-желанию.
Он же пойдет из `.env.local` при сборке через `npm run build`.

```bash
cp .env .env.local
vi .env.local
```

Разработка в режиме hot-reload.

```bash
npm i -g npm@7
npm install -g n
sudo n 15.12.0
# первый раз делаем
npm install
# или так, если видим ошибку
export CXXFLAGS="--std=c++17" && npm install
# затем
npm run dev
```

Далее открываем [http://localhost:3000](http://localhost:3000) - профит.

Перед PR обязательно делать `lint` и `format`.   // TODO
Надо смотреть что бы не оставалось ошибок после линтера.

```bash
npm run lint # чинит и/или показывает ошибки
nom run format # чинит кодстайл
```

## Примерная структура

`/pages` - роутинг, инициализация корневых компонентов, наполнение компонентами

`/components` - сами компоненты

`/public` - статика

`/styles` - scss стили

`/shared` - клиенты к API, стейт, кастомные хуки и утилитные компоненты

`.env` - переменные

`.prettier*, .eslint*` - настройки линтера и форматтера // TODO

## Деплой и CI

Стейджи в деплое
- Тестинг: https://deploy.yandex-team.ru/stages/uchenki-testing
- Прстейбл: https://deploy.yandex-team.ru/stages/uchenki-prestable
- Прод: https://deploy.yandex-team.ru/stages/uchenki-production

Сборка - приложен `Dockerfile` который соберет небольшой контейнер с `nginx` и `node` для рендеринга.
- `nginx` слушает на`:80`
- фронтендовские запросы роутим в ноду на `:3000`
- запросы в `/api/*` роутим в бэкэнд на `:8080`

Ручной деплой (если например что-то разрабатываем и хотим посмотреть на тестинге\престейбле не мерджа в транк)
- собрать докер образ `docker build -t registry.yandex.net/searchmon/uchenki/frontend .` (это сразу пометит образ как `:latest` локально)
- тегнуть как-нибудь уникально, например: `docker tag registry.yandex.net/searchmon/uchenki/frontend:latest registry.yandex.net/searchmon/uchenki/frontend:my-big-feature`
- запушить в репо `docker push registry.yandex.net/searchmon/uchenki/frontend:my-big-feature`
- поменять слой box'a фронтенда в deploy

Деплой через CI
- Заходим в https://a.yandex-team.ru/projects/uchenki/ci/releases/timeline?dir=search%2Fmon%2Fuchenki&id=uchenki-frontend-release
- Нажимаем `run release`
- Пример релиза: https://a.yandex-team.ru/projects/uchenki/ci/releases/flow?dir=search%2Fmon%2Fuchenki&id=uchenki-frontend-release&number=18
- В тестинг покатится автоматом, на прейстейбл и прод нужно снять `manual block`  с кубика
