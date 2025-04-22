# Настройка мониторингов

## Как использовать

1. [Получаем токен](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/monitorado#токены) и кладем в `.env`

1. Устанавливаем зависимости:

        npm i -g @yandex-int/monitorado --registry=https://npm.yandex-team.ru

1. Смотрим, что изменилось:

        monitorado diff -v

1. Обновляем в проде:

        monitorado exec -v

## Полезная информация
Документация по [monitorado](https://github.yandex-team.ru/toolbox/monitorado)

Документация по [флаподаву](https://wiki.yandex-team.ru/sm/juggler/FlapDetector/)

[rum](https://rum.yandex-team.ru/projects/quasar-ui/projectDashboard?filter=environment%20==%20production)
[Ошибки](https://error.yandex-team.ru/projects/quasar-ui/projectDashboard?filter=environment%20==%20production)
[Панель графиков](https://yasm.yandex-team.ru/panel/kingmaniya.quasar-ui)
