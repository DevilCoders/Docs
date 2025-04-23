# Настройка Pulse для сервисов

## Конфиг пульса

Для всех джоб пульса необходимо иметь настроенный конфиг пульса для вашего сервиса в монорепе и конфиг пульса в genisys.

Конфиг в монорепе необходимо положить по пути `<service>/.config/pulse-config.js`, сам формат конфига:
```js
module.exports = {
    static: { // секция для pulse static
        dest: staticDest, // путь до артефакта со статикой
    },
    shooter: { // секция для pulse shooter
        apphostMode: true, // необходимо выставить в true, если ваш сервис работает под Apphost'ом
        shooterRequestLimit: 5000, // количество обстрелов (чем больше число, тем дольше выполняется задача, но точнее результаты)
        dest: dynamicDest, // путь до артефакта с динамикой
    },
};
```

Если вам нужно запускать только Pulse Static или Pulse Shooter, то необходимо указывать соответствующую секцию в конфиге.

Также для запуска необходимо создать конфиг в genisys для вашего сервиса ([пример](https://genisys.yandex-team.ru/rules/pulse.ydo/config)). Для этого необходимо в [#yandex-velocity](https://yndx-all.slack.com/archives/C01FB7ABAD9) попросить создать конфиг с названием, аналогичным названию сервиса в монорепе. [Дока](https://wiki.yandex-team.ru/velocity/serp/pulse/) по настройке конфига.

## Базовый артефакт

Базовый артефакт собирается в джобе `Pulse build` во время мержа вашего ПРа, после успешного мержа базовый ресурс переопубликовывается при помощи [Publish MQ artifacts](../faq/publish-mq-artifacts.md). Т.о. корректно работать проверка будет только после влития ПРа с настройкой пульса в транк(для сравнения размеров бандлов нужен собранный артефакт базовой версии).

Для запуска этой команды вам нужно добавить в ваш `package.json` команду `ci:pulse:build`, при помощи которой ваш сервис будет собирать код и упаковывать его в артефакты (пример команды: `"ci:pulse:build": "YENV=production run-s ci:build artifacts"`). Также вам нужно добавить в конфиг селективности, если он есть, правила для запуска `pulse build` ([пример](https://a.yandex-team.ru/review/2050140/files/5#file-0-97477785:R86)).

[Пример конфига для tartifacts](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo/.config/tartifacts?from_pr=2050140&rev=r8702066) для упаковывания артефактов.

## Static

Для запуска необходимо:
* Настроить секцию `static` в конфиге монорепы, согласно инструкции выше
* Добавить в `package.json` вашего сервиса скрипт `"ci:pulse:static": "npm run ci:pulse:build"`, при помощи которой будет собираться актуальный артефакт. Обычно, кроме сборки артефакта, в этот скрипт еще добавляют анализ бандла bundle-analyzer'ом.
* Настроить секцию `pulse:shooter` в конфиге селективности вашего сервиса аналогично секции `pulse:build`

Пример отчёта работы: ![image](../images/pulse_static__report.png)

## Shooter

N.B. Pulse Shooter работает только для сервисов под RR.

Для запуска необходимо:
* Настроить секцию `shooter` в конфиге монорепы, согласно инструкции выше
* Добавить в `package.json` вашего сервиса скрипт `"ci:pulse:shooter": "npm run ci:pulse:build"`, при помощи которой будет собираться актуальный артефакт
* Настроить секцию `pulse:shooter` в конфиге селективности вашего сервиса аналогично секции `pulse:build`

Инструкция по настройке запуска самого обстрела: https://wiki.yandex-team.ru/velocity/serp/pulse/pulse-in-frontend/

## Shooter memory leaks

Подробнее про саму проверку: https://wiki.yandex-team.ru/velocity/serp/pulse/#obnaruzhenieutechekpamjati

Сейчас проверка запускается только в релизах (т.к. выполнение занимает от полутора до двух часов) на 50к патронов.

Для того чтобы проверка заработала у вас в релизах, вам необходимо подключить Pulse Shooter и добавить в конфиг в genisys секцию с лимитами по памяти под названием memory_limits ([пример](https://genisys.yandex-team.ru/rules/pulse.ydo/config)).

# Поддержка

По всем вопросам подключения Pulse вы можете обратиться в канал [#si_frontend](https://yndx-all.slack.com/archives/CFFAR0VR6).
