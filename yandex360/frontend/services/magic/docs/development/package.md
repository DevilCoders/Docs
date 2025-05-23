# Сборка проекта

**Docker-образ** с приложением собирается и публикуется с локальной машинки командой `make ci-container-publish`. Для сборки нужен `bash` не ниже 5 версии.  
Docker-образ заливается на `registry.yandex.net/mail/magic-front`.

Для сборки пакета используется [Trendbox CI](https://github.yandex-team.ru/search-interfaces/trendbox-ci).
Сборка не происходит локально из-за потребности в секретах для выкладки артефактов сборки в различные окружения.
Артефактов сборки 2:
- **Sandbox-ресурс** с архивом файлов, подкладываемых в docker-контейнер, содержит серверных код и информацию о статике;
- **Статические файлы** сборки, раскладываются на `s3`, проксируются для выдачи клиентам через `yastatic.net`, лежат в бакете `magic`.

Информация о том, какие статические файлы использоватьь для данной конкретной версии выкаченного 
на любое из окружений (тестинг/прод) хранится в генерируемом в процессе сборки статики
файле `webpack-assets.json` и доставляется в контейнер вместе с sandbox-ресурсом.

## Сборка статики

Дев-сборка:
```shell script
npm run build:dev
```
Прод-сборка:
```shell script
npm run build:prod
```

Также при сборке статики можно анализировать получившиеся бандлы, для этого нужно 
раскомментировать в [конфиге webpack](../../webpack.config.js) строку
```javascript
// new (require('webpack-bundle-analyzer')).BundleAnalyzerPlugin()
```

## Сборка пакета

Для запуска процесса сборки нужно запушить в репозиторий тег, после чего github запустит при помощи 
вебхуков саму джобу в trendbox (конфиг джоб можно посмотреть в корне репозитория, в файле `.trendbox.yml`).

Для упрощения процедуры запуска есть команда `npm run package`. Параметры запуска:

`-v` — Конкретная версия для пакета (публикация выполняется с флагом `--force`).
`-t` — Номер релизного тикета. Если не добавить номер тикета, инкрименируется минорная версия, иначе — патч. Номер тикета записывается в комментарий к тегу и коммиту.
`-f` — Публикация с флагом `--force`.

Все дополнительные параметры необходимо указывать через двойное тире (`--`).

**Примеры**:

Публикация минорной версии:
```shell script
npm run package
```
Публикация патч версии с релизным тикетом:
```shell script
npm run package -- -t "MAGIC-123"
```
Публикация конкретной версии:
```shell script
npm run package -- -v "v1.0.0"
```
Публикация конкретной версии с релизным тикетом:
```shell script
npm run package -- -v "v1.0.0" -t "MAGIC-123"
```
