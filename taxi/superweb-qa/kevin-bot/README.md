# Kevin BOT

## Запуск

- [Используемая версия NodeJS](https://a.yandex-team.ru/arc_vcs/taxi/superweb-qa/kevin-bot/.nvmrc)
- [Используемые переменные окружения](https://yav.yandex-team.ru/secret/sec-01g4yy4wgj3wje5g5tpdw3212x/)

```bash
# локальный запуск
npm run start
# с выводом дебага и перезапуском при изменении файлов
npm run debug:mon
```

## Бот

- в проде [t.me/qakevin_bot](https://t.me/qakevin_bot)
- при локальном запуске [t.me/qakevinlocal_bot](https://t.me/qakevinlocal_bot)

```bash setMyCommands
help - Напечатать все команды бота
fleet_create_driver - Fleet: создать водителя
tg_chat - Telegram: получить информацию о чате
```

## Сборка

- [Teamcity](https://teamcity.taxi.yandex-team.ru/project.html?projectId=TaxiInfraArcClownDeployer_KevinSuperwebTestBot&tab=projectOverview)
- [Tariff-Editor](https://tariff-editor.taxi.yandex-team.ru/services/38/edit/357552/deployments?service_name=kevin)
- [Nanny Service Production](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_superweb-test-kevin-bot_stable/)
- [Nanny Service Prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_superweb-test-kevin-bot_pre_stable/)
- [Nanny Service Testing](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_superweb-test-kevin-bot_testing/)
- [Nanny Awacs Production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/superweb-test-kevin-bot.taxi.yandex.net/show)
- [Nanny Awacs Testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/superweb-test-kevin-bot.taxi.tst.yandex.net/show/)
