# Настройка мониторингов

## Как использовать

1. [Получаем токен](https://github.yandex-team.ru/toolbox/monitorado#%D0%A2%D0%BE%D0%BA%D0%B5%D0%BD%D1%8B) и кладем в `.env`

1. Устанавливаем зависимости:

        npm i -g @yandex-int/monitorado --registry=https://npm.yandex-team.ru

1. Смотрим, что изменилось:

        monitorado diff -v

1. Обновляем в проде:

        monitorado exec -v

## Полезная информация
Документация по [monitorado](https://github.yandex-team.ru/toolbox/monitorado)

Документация по [флаподаву](https://wiki.yandex-team.ru/sm/juggler/FlapDetector/)

[Панель графиков](https://yasm.yandex-team.ru/panel/kingmaniya.station)
