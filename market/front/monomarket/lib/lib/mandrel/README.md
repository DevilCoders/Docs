[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/front/monomarket/lib/lib/mandrel/dist&vcs=arc)](https://oko.yandex-team.ru/arc/market/front/monomarket/lib/lib/mandrel/dist) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/mandrel)](https://oko.yandex-team.ru/pkg/@yandex-market/mandrel)

Market mandrel
==============

# Сборка
Чтобы собрать **mandrel**, нужно сделать следующее:
- `npm ci` в корне mandrel
- `npm run build` чтобы собрать файлы с **flow** и получить чистый **javascript**

Для каждого `.js` файла из `src` будет создано два файла в папке `dist`.
Первый это `.js` - скомпилированный **javascript** файл без типов.
Второй это `.js.flow`, и это исходный файл из папки `src`, скопированный сюда
чтобы можно было получить информацию о типах после публикации.

К сожалению, сорс-мапов нет.

# Использование на локальных машинах и логрусе
1. Заходим в mandrel и делаем `npm i` и затем `npm run build`
2. В проекте к которому собираемся подключить данную версию mandrel заменяем в package.json версию пакета на `file:///абсолютный/путь/до/локальной/папки/с/мандрелом/dist`
3. Делаем `rm -rf node_modules/@yandex-market/mandrel`
4. Делаем `npm i` - это поставит свежие зависимости самого mandrel'а в текущий проект.
5. Создаём в корне проекта скриптик с примерно тамим содержимым (пути надо проставить правильные):
```bash
#!/usr/bin/env bash
set -ex

MANDREL_MODULE_PATH="node_modules/@yandex-market/mandrel"
MANDREL_PATH="/абсолютный/путь/до/локальной/папки/с/мандрелом"

pushd ${MANDREL_PATH}
rm -rf dist
npm run build
popd

rm -rf ${MANDREL_MODULE_PATH}
cp -r ${MANDREL_PATH}/dist ${MANDREL_MODULE_PATH}
```
6. Запускаем получившийся скрипт из корня проекта
7. Запускаем сервер как обычно
8. При внесении изменений в мандрел повторно запускаем скрипт

В качестве альтернативного метода можно вместо пунктов 5,6,8 вручную выполнить один раз содержимое указанного скрипта, а затем включить sync с локальной машины из `mandrel/dist` непосредственно в `node_modules/@yandex-market/mandrel` и делать сборку локально.

# Использование на демостенде
Для того чтобы протестировать ветку из **mandrel** на дев окружении сперва нужно выполнить `npm run publish:git`.
Эта команда удалит папку **dist**, прогонит тесты и заново скомпилирует код в **dist**.
После этого содержимое папки **dist** будет опубликовано на **github** в отдельной ветке.
В конце выведется такой текст:


```
Published
Branch name: dev-3b28d4ddfb04b5899d108c1f84eddc7ece448d08
```

Берём имя ветки и добавляем её в **package.json**

```
"@yandex-market/mandrel": "git://github.yandex-team.ru/market/mandrel.git#dev-3b28d4ddfb04b5899d108c1f84eddc7ece448d08",
```

Или из командной строки:

```
npm i --save git://github.yandex-team.ru/market/mandrel.git#dev-9fcf343a885fe0c87396ccf1a5875f6eb9a9acfd
```

Теперь можно запускать сборку дев-окружения

# Публикация
Чтобы опубликовать новую версию **mandrel**, сделайте следующее:
- обновите версию в **package.json**
- выполните `npm run publish:npm` в корне **mandrel**

# Обновление версии в зависимых проектах
- Откройте [sandbox.yandex-team.ru](sandbox.yandex-team.ru)
- Создайте таску с типом MARKET_FRONT_ENVY
- Укажите версию mandrel@new_version_number
- Укажите задачу, в рамках которой происходит публикация библиотеки
- Запустите. В указанной задаче появятся подзадачи, которые отвечают за свой PR в зависимом репозитории
