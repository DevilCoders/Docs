# Подсчет покрытия и дифф в ПРе в unit

[График](https://datalens.yandex-team.ru/luw9wxysy2tge-frontend-coverage) покрытия юнит-тестами кода по транку.

## Настройка

1. Установить пакет [@yandex-int/frontend-jestconfig](../../packages/frontend-jestconfig/) и все его `peerDependecies`
2. Отнаследовать конфига для jest в вашем листе от конфигурации из пакета `@yandex-int/frontend-jestconfig` и по необходимости заоверрайдить нужные поля, кроме поля `coverageReporters` ([пример подключения конфига](../../services/stub/.config/jest/jest.config.js))
3. Добавить/доработать в package.json скрипт `ci:unit`, который будет вызывать jest с флагом `--coverage`
4. Создать по пути `<leaf_name>/.config/coverage.json` файл со следующим содержанием:
```json
{
  "unit": {
    "maxRegressPercent": 1 // нужно указать процент максимально регрессии
  }
}
```
5. Если `maxRegressPercent` равно 0, то в ПРе будет вычисляться регрессия, но проверка не будет падать.

[Пример подключения](https://a.yandex-team.ru/review/2018304/details) в листья с настроенным jest.

Сама проверка начнет работать только после влития ПРа, т.к. эталон по транку загружается только для тех листьев, для которых была выполнена приведенная выше настройка. Эталон хранится 30 дней, поэтому для сервисов, в которые редко коммитят, проверка может не работать или работать некорректно. 

## Просмотр отчета в ПРе

Если все настроено верно, в последующих ПРах в джобе юнитов будет отчет о покрытии для текущего ПРа (`<leaf_name> - ci:unit - report-unit:coverage`) и дифф относительно покрытия в транке (`<leaf_name> - report-unit:coverage-diff_txt`).

Пример отчета о покрытии: ![image](../../images/unit-coverage.png)

Пример диффа относительно покрытия в транке, когда произошла регрессия:
```text
Coverage decreased -2.8% (-11) lines. (total)
Coverage decreased -100% (-7) lines. (src/components/Title/Title.tsx)
Coverage decreased -100% (-4) lines. (src/components/Title/Title@desktop.tsx)
Coverage decreased -100% (-4) lines. (src/components/Title/Title@touch.tsx)
Coverage increased +67% (4) lines. (src/utils/rum/helper.ts)
```
