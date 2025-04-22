# trending-errors-*

- trending-errors-all-backends (alert-523 в error booster) - Trending ошибки во всех бекендах
- trending-errors-java-web (alert-521 в error booster) - Trending ошибки в бекенде java-web
- trending-errors-java-api5 (alert-525 в error booster) - Trending ошибки в бекенде java-api5
- trending-errors-java-intapi (alert-526 в error booster) - Trending ошибки в бекенде java-intapi
- trending-errors-java-jobs (alert-527 в error booster) - Trending ошибки в бекенде java-jobs

## Описание { #description }
Набор алертов, заведённых в [error booster](https://error.yandex-team.ru/projects/direct)

Алерты реагируют на всплески ошибок. Это бывает полезно, если после выкладки очередного релиза (или по другой причине) стало очень много ошибок, и это сильно отличается от обычного фона

При необходимости можно добавить новый алерт или удалить ненужный. Для этого достаточно поредактировать конфиг [direct-apps.conf.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/zk-sync/confs/direct-apps.conf.yaml) (желательно [сделать алерт с понятным названием](../../jeri/guide/solo-name-error-booster-alerts.md))

Если же нужно изменить порог срабатывания отдельного алерта, то это можно сделать прямо на [странице редактирования алертов в error booster](https://error.yandex-team.ru/projects/direct/settings/alerts)

## Диагностика { #diagnostics }
Если загорелась проверка, нужно пойти в [error booster](https://error.yandex-team.ru/projects/direct) и посмотреть, почему сработал алерт

Если количество ошибок действительно сильно выросло, и алерт сработал по делу, то нужно начать разбираться в проблеме

Если же это было ложное срабатывание, то нужно понять, почему алерт сработал, и, возможно, подправить пороги

Для отладки можно воспользоваться ручкой, которая умеет вычислять состояние алерта по ретроспективным данным (на выбранный момент времени)

С вопросами можно обращаться к [elwood](https://staff.yandex-team.ru/elwood)

## Ссылки { #links }
- [Дашборд проекта Direct в error booster](https://error.yandex-team.ru/projects/direct)
- [Все алерты Директа в error booster](https://error.yandex-team.ru/projects/direct/settings/alerts)
- [Вики](https://wiki.yandex-team.ru/error-booster/alerts/) по алертам в error booster
