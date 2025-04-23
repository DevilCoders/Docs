# review-assigner
Скрипт для назначения ревьюеров для код-ревью.
Список ревьюеров берётся из бункера: [auto_ru/common/code-reviewers](https://bunker.yandex-team.ru/auto_ru/common/code-reviewers?view=raw).

## Сборка
1. Апнуть CHANGELOG.md (апать версию можно скриптом [dch-docker.sh](https://github.com/YandexClassifieds/admin-utils/blob/master/dch-docker.sh));
2. Запустить [сборку в TeamCity](https://t.vertis.yandex-team.ru/buildConfiguration/vs_frontend_Applications_AuroRuFrontendRepo_ReleaseShivaAfReviewAssigner);
3. Посмотреть результат в [админке](https://admin.vertis.yandex-team.ru/services/af-review-assigner) и промоутнуть в прод.

