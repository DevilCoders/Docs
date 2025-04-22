# mimino-proxy

С локальных машин разработчиков нет сетевого доступа к blackbox-mimino.yandex.net, что делает невозможным локальную разработку.

### Использование
Замените использование `http://blackbox-mimino.yandex.net` на `http://production.mimino-proxy.metrika-qa.stable.qloud-d.yandex.net`

### Разработка
- Билдим образ - `npm run build`
- Запускаем его - `npm run dev`. После чего вы окажетесь внутри контейнера в папке `/app`
- Внутри контейнера выполнить команду из секции `CMD` из `Dockerfile` - запустится nginx

В контейнер в папку `/app` примонтирована папка с проектом, поэтому изменяя файл `nginx.conf` снаружи он поменяется и внутри контейнера
 
С хоста можно делать запросы в контейнер, например `curl localhost:80/blackbox`

### Сборка и выкладка
Проект живёт в qloud - https://platform.yandex-team.ru/projects/metrika-qa/mimino-proxy/production

- Билдим образ - `npm run build`
- Запушим в registry - `npm run push`
- Деплоим в https://platform.yandex-team.ru/projects/metrika-qa/mimino-proxy/production
