### Примерный текущий алгоритм по переключению версий фронтенда КИ.

Если хочется посмотреть какую-то другую версию фронтенда. Не текущую, например, а в разработке, или какую-то из предыдущих.

1. Смотрим доступные версии тут: https://cm-testing.market.yandex-team.ru/api/frontend/versions

Допустим нужна версия из бранча/задачи MBO-26124

Далее пользователь (пусть будет тестировщик):

2. В консольке браузера выполняет document.cookie = "static_version=MBO-26124;path=/"
3. Перезагружает страничку по F5, например
4. Тестит
5. Возвращает на текущую версию перезапуском браузера

Т.е. переходим по урлу https://cm-testing.market.yandex-team.ru/

открываем консольку, выполняем

document.cookie = "static_version=MBO-26124;path=/"

(Enter не забыть нажать)

F5, работаем с нужной версией

Для возврата на текущую версию перезапускаем браузер

### Скрипты для работы с разными версиями фронтенда
Скрипты позволяют вручную управлять версиями фронтенда на S3.   
Для их запуска нужно установить себе aws-cli: https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html
 
По умолчанию настройка идет на static-mboc-local. При работе с бэком не забыть настроить его для работы с нужным бакетом (market/mbo/mbo-category/mboc-app/src/main/properties.d/local/03-services.properties)

```
mboc.s3.static.bucket=static-mboc-local
```

Собираем фронт

```bash
npm run build
scripts/s3-build-upload.sh
```
После выполнения из строки 
```
uploading to static-mboc-build/005b71f79a3511dc8866c98e221bfc49ea286120 on branch MBO-25973
```
берем ревизию 005b71f79a3511dc8866c98e221bfc49ea286120

Используем ревизию в команде
```bash
scripts/s3-build-deploy.sh 005b71f79a3511dc8866c98e221bfc49ea286120
```
Устанавливаем текущей версией
```bash
scripts/s3-set-current-version.sh 005b71f79a3511dc8866c98e221bfc49ea286120
```

Теперь бэк при обращении к http://localhost:8080 будет отдавать текущую (или форсированную) версию

Форсировать версию
```bash
scripts/s3-set-force-version.sh 005b71f79a3511dc8866c98e221bfc49ea286120
```

Сбросить форс версии
```bash
scripts/s3-clear-force-version.sh
```
