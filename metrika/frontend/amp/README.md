# AMP

## Локальная разработка

Быстрый старт:

```
npm ci
```

Запуск проекта:

```bash
npm run server
npm start
```

Запуск проекта в режиме разработки:

```bash
npm run server
npm run dev
```

Сборка проекта:

```bash
npm run build
```

## Шаблоны

Моковые AMP страницы собираются при помощи `npm run build`. Для добавления шаблона, нужно в скрипт `./scripts/build.js`
в переменную `presets` добавить `renderer`. `renderer` нужно положить в `./src/renderers/<имя>`. Сами шаблоны лежат
в папке `src`.

Пресеты - это своего рода сборки страниц на разную тему, например: бесконечная лента, карусель, просто статья и тд.

Шаблонизация происходит при помощи замены переменных вида `{{VARIABLE}}` значениями или другими шаблонами.

Для просмотра отрендереных шаблонов, нужно запустить локальный сервер `npm run server`. Сервер запуститься на порту 3000,
после чего перейти к готовой страничке можно по урлу: `http://localhost/dist/<имя-пресета>/<имя-файла>`.

## Подмена AMP скрипта

Интеграция для метрики живет в [AMP репозитории](https://github.com/ampproject/amphtml/) (в файле
`./extensions/amp-analytics/0.1/vendors/metrika.json`). Может возникнуть ситуация при которой этот файлик захочется
изменить и посмотреть как эти изменения поведут себя на готовых страничках (как на заготовленных страничках в этом
репозитории, так и на реальных сайтах). В таком случае нужно подменить этот `metrika.json` файл вместо продовского на
локальный по следующему флоу:
- для начала форкаем, клонируем и собираем AMP проект:
  - [гайд](https://github.com/ampproject/amphtml/blob/master/contributing/contributing-code.md)
  - [гайд поменьше](https://github.com/ampproject/amphtml/blob/master/contributing/getting-started-quick.md)
- `npm run build` и запускаем локальный сервер из AMP репозитория (как написано в гайде выше)
  - локальный сервер AMP репозитория запускается на порту 8000
  - посмотреть как дела у нашей интеграции можно перейдя в `analytics-vendors.amp.html` (выбираем vendor metrika и жмем Go)
- делаем нужные нам изменения в AMP репозитории
- стартуем прокси `npm run proxy` уже из этого репозитория
- прокся запускается на порту 8888, меняем сетевые настройки чтобы рабочий ноут использовал локальную проксю
- после этого, прокся будет редиректить запросы за продовским `metrika.json` (он живет на cdn) на локальный
  сервер запущенный из AMP репозитория на порту 8000, таким образом изменения сделанные в AMP репозитории будут
  доступны на всех сайтах (включая локальный сервер в этом репозитории)

__Важно:__ так как AMP сервер не знает что его проксируют, он не будет пересобирать локальный `metrika.json` пока ему
самому он не понадобится, по этому чтобы увидеть изменения в `metrika.json` из под прокси иногда может понадобится зайти
сначала на локальный AMP сервер чтобы он переесобрал бандл (т.е. сначала нужно сходить например на
`http://localhost:8000/examples/analytics-vendors.amp.html?type=metrika`).

## Порты

- `8000` сервер AMP
- `8888` mitmproxy
- `3000` метричный сервер с шаблонами для AMP

__Важно:__ все запросы делаем на счетчик `71129776`

## Полезные ссылки

- [Create your first AMP page](https://amp.dev/documentation/guides-and-tutorials/start/create/?format=websites)
- [Integrate your analytics tools in AMP HTML](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/integrating-analytics.md)
- [AMP HTML URL Variable Substitutions](https://github.com/ampproject/amphtml/blob/master/spec/amp-var-substitutions.md)
- [Installing and setting up a tag on a site with AMP](https://yandex.com/support/metrica/code/install-counter-amp.html)
- [AMP счетчик в Метрике `71129776`](https://metrika.yandex.ru/dashboard?id=71129776)
