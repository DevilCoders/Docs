# Чеклист запуска нового сервиса

1. Развернуть сервис из [стаба](../../services/stub/README.md).
2. Настроить логирование при помощи [Яндекс.Метрики](https://yandex.ru/support/metrica/general/creating-counter.html) и/или [Баобаба](../../packages/react-baobab-logger/docs/quick-start-react.md)
3. Определить список поддерживаемых браузеров, для прочих настроить [лендинг](../../packages/page-for-outdated-browsers/README.md)
4. Убелиться в актуальности [csp-политик](https://wiki.yandex-team.ru/product-security/csp/)
5. Пройти [аудит безопасности](https://wiki.yandex-team.ru/product-security/audit/)
6. Убедиться, что сервис корректно [локализован](https://wiki.yandex-team.ru/l10n/localization-policy/l10nnew/) и соответствует стандартам [доступности](https://wiki.yandex-team.ru/lego/a11y/)
7. Настроить мониторинги, [создать алерты на ошибки из Error Booster](https://wiki.yandex-team.ru/error-booster/alerts/)
8. Подключить асессоров к [тестированию релизов](./crowdtesting-from-pr.md)
9. Выкать apphost-граф в hamster/production (//todo)
10. Выкатить первый релиз в продакшен по [инструкции](./setup-releases.md)

Полный [чеклист запуска нового сервиса](https://wiki.yandex-team.ru/projectmanagement/um/checklist)
