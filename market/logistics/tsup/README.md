## TSUP
Центр управления перевозками. Бэкэнд для кабинета логиста.

Для запуска компонента необходимо заполнить в String boot:
- VM options:  `-Dspring.profiles.active=local`
- Working directory: `$MODULE_WORKING_DIR$`
- Environment variables: `PROPERTIES_DIR=<абсолютный путь до properties.d в arc>`
- создать файл `src/main/properties.d/local/application.properties` (рядом есть соответствующий .dist файл)

Перед запуском запустить стабы
`cd dependency-stub && docker-compose up -d`

### Redis & Sandbox
При первом запуске вам может понадобиться подгрузить актуальный embedded-redis из sandbox
Для этого необходимо:
- создать файл `src/integration-test/resources/application-local.properties` (рядом есть соответствующий .dist файл)
- записать в него OAuth токен, полученный в https://docs.yandex-team.ru/sandbox/api#auth-oauth


### IDEA http client
Для выполнения запросов к бэкендам магистральной платформы можно использовать встроенный http client в IDEA
Для этого необходимо:
- создать файл `http/requests.http` (рядом есть соответствующий .dist файл)
- из него можно запускать запросы или генерировать curl

