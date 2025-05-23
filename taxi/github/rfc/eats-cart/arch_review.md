# Опросник для ревью комитетом

## Название сервиса

eats-cart

## Какую продуктовую проблему решает сервис?

Выносит часть логики из монолита Еды, разблокирует возможность продуктовых доработок.

## Почему нельзя решить эту задачу без разработки нового сервиса существующими решениями?

Потому что монолит на php, мы его распиливаем.

## Как именно сервис будет решать поставленные перед ним задачи?

Будет инкапсулировать логику сбора, хранения и отдачи корзины.

## Разрабатывается один сервис или система?

Один сервис

## С кем взаимодействует сервис?

- Получает информацию о ресторане, сурже, стоимости доставки из eats-catalog
- Получает информацию о блюде для ресторанов из Коры (пока нет отдельного хранилища)
- Получает информацию о товаре для ритейла из eats-products
- Получает информацию об активных акциях из коры

В кору делаем одну попытку запросить данные, кешируем у себя данные в redis и используем в ручке получения корзины.

Для запроса информации о ресторане делаем 2 ретрая, если не получилось — отдаём ошибку.

При недоступности меню на изменяющих ручках, фолбечимся на данные из redis.

При недоступности акций, акции не применяются, остальное работает штатно.

## Какие базы использует?

Будет использоваться PGaaS, redis.

## Какие периодические процессы?

В будущем: очистка старых корзин, репликация старых корзин в YT.

## Прикрепите схему того, где этот сервис находится в текущей инфраструктуре

1. **Как технически проект влияет на цикл заказа.**
Клиенты будут переключены на ручки нового сервиса через api-proxy по эксперименту.
По этому же эксперименту на получение данных из нового сервиса будет переключена логика создания ревизии заказа (order_revision) из корзины на чекауте.
1. **Кто будет потребителями сервиса.**
Чекаут, клиенты.

## Какие данные и по какой схеме сервис будет хранить в базе?

Хранить будем посчитанную стоимость корзины, набор блюд в ней с зафиксированными ценами и набор применённых акций, промокодов, выбранные опции блюд.

Также будет храниться связка пользователь-корзина. Сейчас клиентское API должно гарантировать что у одного пользователя будет только одна корзина, поэтому тут будет индекс по id пользователя.

## Какой объем данных будет храниться и какой объем будет изменяться в единицу времени?

Объем хранимых данных, как их подразумевается чистить. Ресурсы под СУБД (cpu, ram, disk).

Для оценки объёма redis считаем что храним данные с ttl 1 час, размер одной записи 5KiB, за час в корзину добавляется около 50k уникальных айтемов (посмотрел по боевой реплике). Итого 255 MiB.

На обновление ожидается не более 20 qps, на чтение 50 qps. Должно хватить m2.nano.

Для оценки объёма постгреса можно ориентироваться на текущий размер таблиц корзины (чистили 10.02.2021 руками). За это время накопилось 4GiB данных. Соответственно, за год будет около 50 GiB. Дальше подумаем над автоочисткой и репликацией в YT.

По нагрузке будет 30 qps на запись и 80 qps на чтение. Думаю что флейвора s2.nano должно хватить. Если что, переключать будем плавно и подкинем железа.

## Какая нагрузка ожидается?

Ожидается нагрузка порядка 100RPS на все ручки.

- `~ 50` rps на получение корзины
- `~ 20` rps на добавление айтема
- `~ 1` rps на синхронизацию корзины
- `~ 5` rps на изменение айтема
- `< 5` rps на удаление айтема
- `< 1` rps на применение промокода
- `< 1` rps на удаление недоступных айтемов/акций
- `< 5` rps на удаление корзины

## Какие фолбеки предусмотрены на сам этот сервис?

Фолбека нет: при недоступности сервиса невозможно положить блюдо в корзину.

При проблемах в первое время можно будет отключить сервис и вернуть нагрузку в старую корзину.
Дальше нужно будет продумывать фолбек на локальное хранение корзины на клиентах при недоступности сервиса.

## Какие возможности масштабируемости закладываются?

Горизонтальное масштабирование сервиса, вертикальное масштабирование базы.

## Какие точки отказа есть в сервисе?

PGaaS, eats-catalog, eda-core, eats-products

## Укажите ключевые продуктовые метрики сервиса, за которыми планируете следить

Конверсия из создания корзины в чекаут, доля отмен.

## Укажите технические метрики

Тайминги, не двухсотые ответы, количество созданных корзин, количество ошибок на создании заказа.

## Какая функциональность ожидается в сервисе в будущем?

Этапы разработки:

1. Разработка mvp решения, повторяющего api текущей корзины
1. Переключение пользователей на новую корзину
1. Улучшение взаимодействие клиентов с корзиной, реализация идемпотентности, проработка и реализация фолбеков при недоступности сервиса корзины.
1. Реализация продуктовых фич в новой корзине


## Какое изменение нагрузки планируется?

Рост пропорционально росту Еды.

## Активно ли будет изменяться сервис?

Да
