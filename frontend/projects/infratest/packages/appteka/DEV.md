# Инструкция для разработчика appteka

## Как собрать

  * `npm i`
  * `npm run build`

## Как разрабатывать

  * `npm run watch`

## Как собрать пакет для выкладывания в nanny-сервис

  * `npm run upload`

## Как обновить апптеку в yatool после изменений

1. Выполнить команду `npm run upload` на OS Linux и OS Darwin, получить 2 `taskId` Sandbox задачи.
2. Перейти в таски и прожать в них кнопки `Release`, чтобы в атрибутах ресурсов появилось поле `released: stable`.

Автообновление происходит раз в день, проверить сразу у себя локально можно с помощью команды `ya tool appteka --force-update`.

## Тестирование

Из-за того, что для тестирования апптеке необходимо делать запросы к SeTrace, тесты не всегда успевают пройти в указанный лимит времени, поэтому большинство из них отмечены опцией `.skip` для успешного прохождения тестов при влитии в Аркадию.
Во время локального тестирования `.skip` нужно убрать и, возможно, запустить упавшие тесты несколько раз (скорее всего, SeTrace просто не успел ответить).
