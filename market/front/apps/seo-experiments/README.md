# seo-experiments

## Разработка

```bash
npm i
npm start
```

Сайт откроется на localhost, при разработке могут быть проблемы с CORS. Обходится через отключение проверки на CORS при запуске браузера.

## Как обойти проблему корсов?

Открыть браузер с отключением корсов
```bash
open -n -a /Applications/Chromium.app/Contents/MacOS/Chromium --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security
```

### Как залить админку?

1. Билдим проект `npm run build`
2. Коммитим содержимое папки build в аркадию https://a.yandex-team.ru/arc/trunk/arcadia/market/seo/experiments/admin/
(Как коммитить в arc: https://doc.yandex-team.ru/arc/index.html)
3. Создаём тут релиз https://tsum.yandex-team.ru/pipe/projects/seo/delivery-dashboard/seo-exps

## Как ходить за запросами в прод?

Поменять константу тут: https://github.yandex-team.ru/market/seo-experiments/blob/master/src/helpers/index.tsx#L20
