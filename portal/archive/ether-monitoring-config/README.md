## Current Aggregate checks
[tag=morda-ether-alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmorda-ether-alerts)

[tag=ether-vh-alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dether-vh-alerts)

[tag=ether-alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dether-alerts)

[tag=morda-vh-alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmorda-vh-alerts)

[tag=morda-alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmorda-alerts)

[tag=vh-alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dvh-alerts)

[tag=marty](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmarty%26namespace%3Dportal)


# Настройки мониторингов для проектов локализации и документации

## Как использовать

1. [Получаем токены](https://github.yandex-team.ru/toolbox/monitorado#%D0%A2%D0%BE%D0%BA%D0%B5%D0%BD%D1%8B) и кладем в `.env`

1. Устанавливаем зависимости:

        npm run deps
    
1. Смотрим, что изменилось:

        npm run diff

1. Проливаем:

        npm run exec
        
1. Коммитим:

        Срабатывает прекоммит хук npm run diff
        
1. Пушим:

        Срабатывает прекопуш хук npm run exec
        
Для мелких изменения руками можно не вызывать команды, а пользоваться хуками

## Полезная информация
Документация по [monitorado](https://github.yandex-team.ru/toolbox/monitorado)

Доступные сигналы из [error-counter](https://github.yandex-team.ru/rum/error-counter#%D0%B3%D0%BE%D0%BB%D0%BE%D0%B2%D0%B0%D0%BD-yasm)

[Сигналы доступные в monitorado](https://github.yandex-team.ru/toolbox/monitorado/blob/error-booster/src/yasm/alerts/builders/project.ts#L14-L24)

По вопросам можно в [telegram](https://telegram.me/orloffv)
