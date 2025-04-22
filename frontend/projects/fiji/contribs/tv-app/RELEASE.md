# Описание процесса релиза

Если релизить нужно одновременно и ресурсы из этого проекта, и само ТВ-приложение,
то нужно придерживаться процесса, описанного
[здесь](https://github.yandex-team.ru/desktop/tv-app/blob/master/RELEASE.md#%D0%9C%D0%B0%D0%B6%D0%BE%D1%80%D0%BD%D1%8B%D0%B9-%D0%B0%D0%BF%D0%B4%D0%B5%D0%B9%D1%82).

## Обновление только скриптов `loader.js` и `main.js`

Вся архитектура нашего приложения построена таким образом,
чтобы этот вариант был основным при обновлении нашей логики.

Шаги:
1. Отводим релизную ветку с названием `release/tv-app/vx.x.x`, где `x.x.x` - версия для релиза
2. Поднять версию этого проекта и поменять в [конфиге](/contribs/tv-app/src/loader/config/index.js)
   лоадера строку(-и) для версий ТВ-приложения, которые должны будут загружать новую версию скрипта `main.js`.
3. На teamcity настроена автоматическая
   [сборка](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Elements_TvAppMain_Build)
   с релизных веток, которая выкладывает скрипты `loader.js` и `main.js` в тестовый бакет нашего s3.
4. Проверить работу новых версий `loader.js` и `main.js` на тестовой сборке ТВ-приложения.
   
   Также можно явно указать новый `main.js` в параметре `js`
   на странице [TV App Launcher](http://myt3-f52ba0bc9d3f.qloud-c.yandex.net/),
   если очень хочется посмотреть его работу на прод-сборке ТВ-приложения.
   Ссылка на новый `main.js` будет `https://tv-app-test.s3.yandex.net/tizen/vx.x.x/main.js`
   (`x.x.x` заменить на версию релиза).
5. Запинить проверенную сборку в [teamcity](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Elements_TvAppMain_Build)
6. Запустить
   [teamcity-сборку](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Elements_TvAppMain_UploadToProd)
   выкладки скриптов `loader.js` и `main.js` в продакшен-бакет нашего s3.
   
   Примечание: скрипт `loader.js` будет переименован в `loader.beta.js`
   для финального тестирования новой версии на продакшене.
7. Провести регрессию на прод-сборке ТВ-приложения, указав в параметре `js`
   на странице [TV App Launcher](http://myt3-f52ba0bc9d3f.qloud-c.yandex.net/) новый `loader.beta.js`.
   Ссылка на новый `loader.beta.js` будет `https://tv-app.s3.yandex.net/tizen/loader.beta.js`.
8. Запустить
   [teamcity-сборку](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Elements_TvAppMain_RenameLoader)
   резервного сохранения (`loader.js` -> `loader.bak.js`)
   и подмены текущего `loader.js` (`laoder.beta.js` -> `loader.js`).
   
   Теперь все клиенты будут загружать новый `loader.js`,
   который для актуальных версий ТВ-приложения загружает новый `main.js`.
9. Проверить работу прод-сборки ТВ-приложения, не передавая никаких параметров запуска -
   открывая его с помощью ТВ-пульта. Загружаться должны новые `loader.js` и `main.js`.
10. Убедиться по метрикам, что ничего не поломалось.

## Ручные npm-команды для релиза
В случае каких-либо проблем с teamcity можно выполнить пп. 3, 6 и 8 локально.

- Выкладка скриптов в тестовый бакет s3, для teamcity
```
npm run release:upload:test
```

- Выкладка скриптов в продакшен-бакет s3, для teamcity
```
npm run release:upload:prod
```

- Смена текущего лоадера в продакшен-бакете s3, для teamcity
```
npm run release:rename
```