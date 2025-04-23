Services and dependencies of Classified Services
===========================

Данный репозиторий содержит вручную составленные машиночитаемые описания всех существующих в Вертикалях сервисов. 

Подробнее про [карту сервисов](https://docs.yandex-team.ru/classifieds-infra/service-map) и [манифест деплоя](https://docs.yandex-team.ru/classifieds-infra/deploy/manifest) можно прочитать в документации [Инфраструктуры Яндекс.Вертикалей](https://docs.yandex-team.ru/classifieds-infra/)

На основе карты будет запущена [автогенерация окружения](https://docs.yandex-team.ru/classifieds-infra/auto).

Она также пригодится для деплоя, проверки sla, мониторинга, прогонки интеграционных тестов, уведомления ответственных и т.п.

[Визуализация зависимостей](https://s3.mdst.yandex.net/vertis-share/services/index.html)

Добавления и изменения происходят через pull request

## Валидация

В каждый PR придет `shivarobot`:
- укажет на ошибки, которые нужно исправить
- призовет ответственных за сервис и попросит у них approve
- выдаст набор предупреждений о deprecated полях и прочем (их лучше сразу исправить)

При необходимости **перезапросить ревью** у робота, нужно перезапустить проверку `VertisAdmin_ArcadiaPr_Validate` в интерфейсе Аркадии
