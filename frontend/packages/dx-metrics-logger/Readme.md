# DX metrics logger

Библиотека помогает логировать все метрики, связанные с процессом разработки.
Есть возможность писать метрики в ClickHouse-кластер, или только в консоль для отладки.

Для добавления логирования метрик в проект необходимо:

## Добавить обработчик запросов в микросервис и создать соответствующую таблицу

Можно делать по аналогии с [этим коммитом](https://github.yandex-team.ru/search-interfaces/microservices/commit/03190a99e1d5d7089f5ae467694fc6d11c5593f5).

## Добавляем в проект
Устанавливаем зависимости.

```(bash)
npm i -D @yandex-int/dx-metrics-logger
```

Дальше добавляем код создания логгера. Стоит создавать один экземпляр логгера на проект.
```(javascript)
import { DxMetricsLogger } from '@yandex-int/dx-metrics-logger';


// Данное значение должно совпадать с ключом созданным на предыдущем шаге
// в services/webhook-handler/modules/metrics-logger/handlers.js
const handler = 'Your_handler_name';

export const dxLogger = new DxMetricsLogger(handler);
```
### Логирование метрик

После этого можно производить замеры шагов DX

```(javascript)
import { dxLogger } from './dxLogger';


function someOperation() {
    // Перед началом операции отмечаем о начале.
    const timer = dxLogger.startTimer('operation_name');

    // Some actions...

    // После операции логируем время выполнения.
    timer.logMetric()
}
```

Метрики можно логировать 2-мя способами:
1. отправлять метрики на сервер и логировать время `.logMetric()`
2. не отправлять на сервер, а при переменной окружения `DX_DEBUG=1` выводить значение в консоль `.debugMetric()`

## Создаём графики

Для отображения залогированных метрик и построения по ним графиков можно в сервисе datalens.yandex-team.ru

[Пример реализации графиков DX метрик команды Архиконтура Серпа.](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/ci/charts/arcadia-frontend-infra/arch-dx)

[Сами графики находятся тут.](https://datalens.yandex-team.ru/navigation/90hpugu7yfey5-arch-dx)

## FAQ

### Как залогировать метрики до установки зависимостей

Действительно, до установки зависимостей нельзя использовать пакет dx-metrics-logger.
Такая ситуация может возникнуть, например, для логирования времени установки зависимостей `npm ci`
Для логирования в этом случае необходимо измерить время вручную, а только потом подключить пакет и воспользоваться методом `logMetric()`.

```(javascript)
const { execFileSync } = require('child_process');

// Отмечаем начало операции
const startTime = Date.now();

// Устанавливаем зависимости
execFileSync('npm', ['ci'], { stdio: [0, 1, 2] });

// Замеряем время операции
const spendTime = Date.now() - startTime;

// зависимости установились, можно использовать
const logger = require('./dxLogger');

// Логируем значение метрики и отправляем результат на сервер
logger.logMetric({ name: 'install-deps', value: spendTime });
```
