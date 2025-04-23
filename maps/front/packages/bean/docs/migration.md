# Как мигрировать существующие шедулеры карт

Для того, чтобы мигрировать существующий шедулер, нужно:

1) установить `@yandex-int/bean` в проект
2) добавить `preversion` и `postversion` хуки в `package.json`
3) обновить `lama.yaml` на использование пресета `preset: projects/maps-front/binary-scheduler`

Пример пулл-реквеста: https://github.yandex-team.ru/maps/infra/pull/538

## У моего шедулера кастомный воркфлоу

Тогда помимо шагов выше укажите `workflow_id` в `lama.yaml` и замените кубик [Maps.Front Github Scheduler](https://beta.nirvana.yandex-team.ru/operation/ea2e4ae2-0e67-483a-8276-2c1f5e145b2e) на [Maps.Front Run binary scheduler](https://beta.nirvana.yandex-team.ru/operation/b132b2a0-08ce-4a97-a54d-a5552793ef89) и свяжите его параметры с глобальными опциями как в этой [операции](https://beta.nirvana.yandex-team.ru/flow/9e21896c-bb79-474f-938d-852d9e496876/53470723-2785-472d-8e91-4b97fc093c26/graph/FlowchartBlockOperation/c8c9c8ab-53f1-47a4-b248-9231c15b6280).