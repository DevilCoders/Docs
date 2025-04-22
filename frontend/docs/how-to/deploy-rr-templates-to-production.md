## Первый деплой шаблонов report-renderer в продакшее

Шаги для деплоя шаблонов:

- Собираем шаблон
- Создаем новый тип ресурса для шаблона
- Деплоим в продакшен

### Собираем шаблон

Для начала надо ознакомиться со [структурой шаблона для report-renderer](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/templates-api/). Примеры таких файлов в UGC:
- [Шаблон — Node.js модуль](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/ugc-pages/src/server/renderer.js)
- [Конфигурация шаблона](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/ugc-pages/.config/templates/config.json)
- [Конфигурация пакета шаблонов](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/ugc-pages/routes.json)

Дальше пишем код в файле шаблона, который отдает html.

После этого шаблон нужно собрать вашим сборщиком ([пример webpack конфига](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/ugc-pages/.config/webpack/server/index.js)) и получить архив вашего шаблона (tar.gz). [Пример npm скрипта который собирает финальный архив](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/ugc-pages/package.json#L6) и [конфиг-описание что положить в архив для report-renderer](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/ugc-pages/.config/tartifacts/dynamic.js)

**Итог:** у вас есть npm скрипт который собирает архив для report-renderer.

### Создаем новый тип ресурса для шаблона

Для этого достаточно воспользоваться командой `update-package` из пакета [apphost-service](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/apphost-service#update-package). Главное чтобы название типа ресура совпадало с id в [этом файле конфига](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/ugc-pages/routes.json)

### Деплоим в продакшен

- У вас в сервисе есть файл `.config/release.json`, подробнее про него [тут](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/release-setup.md). Совет: добавьте всех членов команды в followers для релизной таски, будет полезно в будущем.
- Вы проставили своему сервису первый тег, иначе машинерия не может найти дифф между версиями, как [читаем тут же](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/release-setup.md#%D1%82%D0%BE%D1%87%D0%BA%D0%B0-%D0%BE%D1%82%D1%81%D1%87%D1%91%D1%82%D0%B0-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B9)
- Вы дали нужные права нужным роботам, каким и как читаем [тут](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/ci-integrations.md).
- Теперь можно вручную отвести свой 1 релиз с помощью формы отведения релизов, как читать [тут](./release-form.md).
- Где-то в течении получаса релиз соберется - это будет таска в SB с type `NANNY_RELEASE_RESOURCE` и вашим тегом. Найти ее в SB можно [по фильтру](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=NANNY_RELEASE_RESOURCE)
- Дальше пишем дежурному по report-renderer через [форму](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/duty/). Пишем следующее:
```
Привет, мне нужно настроить Ticket integration для нового сервиса в монорепе.

{Краткое описание сервиса}

- Вот релиз моего шаблона: {вставляем ссылка на вашу таску NANNY_RELEASE_RESOURCE из прошлого шага}
- Вертикаль моего сервиса: {ваша вертикаль, например SHARED}
- Мой продакшен граф: {ссылка на ваш прод граф в Horizon}
- Бэта моего сервиса: {В идеале сделайте простой ПР там поднимется бэта, приложите эту бэту сюда}
```
Отправляем форму, и в ближайшее время дежурный с вами свяжется, если нужно задаст доп. вопросы. Он настроит вам необходимую машинерию.

После этого надо протестировать свой релиз на приемке.
Затем перевести свою релизную таску в статус `Ready for production`([подробнее про статусы](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/release.md#%D0%B2%D1%8B%D0%BA%D0%BB%D0%B0%D0%B4%D0%BA%D0%B0-%D0%B2-%D0%BF%D1%80%D0%BE%D0%B4%D0%B0%D0%BA%D1%88%D0%B5%D0%BD)),
это проставит вашему ресурсу тэг `stable` и после этого он будет готов для релиза на продакшен окружение.

После того, как дежурный report-renderer настроил интеграцию следующие релизы шаблонов можно выкатывать самостоятельно.
Инструкция для раскатки шаблонов в продакшен лежит [на вики](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/selfduty/#relizyvshared).
Подробности про релизный процесс в целом [тут](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/release.md)
