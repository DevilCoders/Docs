# Обзор способов передачи метрик в Solomon

<small>Таблица 1 — Сравнение Pull и Push режимов передачи метрик в Solomon</small>

Характеристика | Pull | Push
---------------|------|-----
Объем передаваемых данных | *Много* данных:<ul><li>Более 10 000 метрик с одного хоста;</li><li>Более 100 хостов в кластере.</li></ul>| *Мало* данных: общий объем до 5 000 метрик в секунду.
Сетка | |
Вычисление [агрегатов](../concepts/aggregation.md#aggregation-on-write)|<span style="color: green;">Точный</span> расчет агрегатов.|Потенциально <span style="color: red;">неточный</span> расчет агрегатов.
Удобство отладки | <span style="color: green;">Удобная диагностика</span>: при каждом запросе к сервису Solomon сохраняет статус запроса и [тип ошибки](https://wiki.yandex-team.ru/solomon/userguide/faq/#chtooznachajutoshibkivsborkesensorov) (если она произошла), что позволяет быстро определить причину проблем. | <span style="color: red;">Затруднённая диагностика</span>: для определения причины проблем необходимо подробное логгирование на стороне клиента.
Поддерживаемые [типы метрик](../concepts/data-model.md#metric-kinds) | Поддерживаются  <span style="color: green;">все типы метрик</span>| Запись `RATE` и `HIST_RATE` метрик <span style="color: red;">не поддерживаются</span>.
Поддерживаемые форматы данных |<ul><li>[JSON](./dataformat/json.md)</li><li>SPACK</li><li>Prometheus</li></ul> | <ul><li>JSON</li><li>SPACK</li></ul>
Гарантии на скорость ответа | |

# Pull-режим {#pull}

## Pull из клиентского приложения {#pull-from-app}

## Pull из клиентского приложения с буферизацией {#pull-with-timeseries}

## Pull из Solomon Agent {#pull-from-agent}

# Push-режим {push}

## Push в Solomon API {#push-api}

## Push в локальный Solomon Agent {#push-to-agent}
