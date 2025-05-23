# Merge Queue Spotlight

> Зеркало очереди в Merge Queue с возможностью предсказания времени до влития пулл-реквеста.

## Что это такое?

Это сервис, отображающий очередь пулл-реквестов в Merge Queue с возможностью предсказания *приблизительного* времени до влития каждого активного пулл-реквеста.

> **Внимание**
>
> Сервис имеет погрешность в величину, которую может дать наличие или отсутствие прогревочной задачи. Предсказание является достаточно точным, если прогревочные задачи равномерно покрывают последние N пулл-ревестов. Более подробнее ниже.

## Страницы сервиса

  * `/` – Главная страница. Выбор проекта и вида отчёта
  * `/:project` – Минималистичное отображение очереди
  * `/report/:project` – Полный отчёт по очереди

## Отличия вариантов отображения

Минималистично отображение очереди подойдёт для конечных пользователей – ничего лишнего. Полный отчёт пригодится командам инфраструктуры, например, для мониторинга на телевизорах. Также в полном отчёте имеется подсветка перезапущенных MQ-задач (был изменён `dev`): персиковый – второй запуск, красный – третий запуск.

## Как это работает?

  * Делается выборка в N последних MQ-задач для проекта.
  * Обработка выборки:
    * Получаем аудит времени для каждой задачи
    * Считаем время в очереди, как разница между статусом после `ENQUEUED` (или текущим временем) и статусом `DRAFT`
    * Считаем время выполнения, как разница между финальным статусом (или текущим временем) и статусом `PREPARING`
    * Считаем полное время задачи, как сумма времени выполнения и времени в очереди
  * Вычисляем среднее время на одну задачу:
    * В расчёте участвуют задачи в статусах `SUCCESS` и `FAILURE` для уменьшения погрешности
    * Считаем среднее время на очередь для одной задачи
    * Считаем среднее время выполнения для одной задачи
  * Формируем очередь и предсказываем время до влития

### Формирование очереди

Перед тем как начать вычислять время до влития, все задачи делятся на три вида:

  * Выполняющиеся
  * Ожидающие в очереди
  * Завершённые

Далее вычисляется время до влития для выполняющихся задач по формуле:

> t<sub>μ выполнения</sub> - t<sub>текущего выполнения</sub>

В этой формуле:

  * μ – Среднее время выполнения для одной задачи

Время до влития для ожидающих в очереди задач вычисляется по формуле:

> i × t<sub>μ выполнения</sub> - ∑t<sub>текущего выполнения</sub> + C

В этой формуле:

  * i – Порядковый номер в очереди
  * μ – Среднее время выполнения задачи
  * ∑ – Сумма текущего времени выполняющихся задач
  * C – Константа времени на Sandbox. Здесь это 1 минута

## Как собрать?

В соответствии с инструкцией разработки в монорепозитории infratest:

```
pnpm i --filter {.}...
pnpm build --filter {.}..
```

## Как запустить?

  * `npm start`

## Как разрабатывать?

  * `npm run watch`

## Как собрать Docker-образ?

  * `make docker-build`

## Как запустить Docker-образ?

  * `make docker-build` – копируем SHA образа
  * `docker run -p 3000:3000 SHA`
  * `safari http://localhost:3000`

## Как зарелизить?

* [Релиз сервиса](docs/release.md)
