# Как выгружать из финстаты большое кол-во событий

## Status

accepted

## Context
Для отчётов дилеров нужно выгружать все события дилеров, сгруппированные
по продукт+день+id оффера за какой-то длинный период. От месяца до года.
У самого крупного дилера таких агрегатов 41к за месяц.
Финстата плохо приспособлена для подобной выгрузки событий, она хорошо подходит для подсчёта более крупных агрегатов.

О каких решениях подумали:
1. С помощью endpoint-a, который отдаёт список сырых событий выгружать все события, постранично.
Этот вариант ок - но нужно на стороне команды-потребителя агрегировать их самим.
2. Делать агрегацию на стороне финстаты, отдавать результаты в стриме
3. Делать агрегацию на стороне финстаты, отдавать результаты в постранично (getSpendings с пагинацией).
   При этом по каждому дню делать запросы отдельно.
4. Выгружать большое кол-во данных не из clickhouse, а из yt. Внутри сервиса финстата.
5. Выгружать большое кол-во данных не из clickhouse, а из yt. Не из финстаты, а сразу сервисом команды потребителей.
6. Добавить ещё одно хранилище, возможно реляционную базу, которая хорошо справляется с подобными запросами.

## Decision
Выбрали вариант 3 - Делать агрегацию на стороне финстаты, отдавать результаты в постранично.
Он достаточно удобен и для разработки финстаты и для команды-потребителя. Не требуется большого кол-ва
времени для имплементации.
Почему нужно делать запросы по каждому дню отдельно:
Запрос построен так, что если указать большой период, данные не помещаются в память кликхауса.
У кликхауса есть ограничения на размер данных в запросе. 
Выглядит что это не проблема запроса, а ограничение кликхауса. 

Почему нет:
1. С помощью endpoint-a, который отдаёт список сырых событий выгружать все события, постранично.
   Этот вариант ок - но нужно на стороне команды-потребителя агрегировать их самим.<br/>
   Это не удобно для команды-потребителя.
2. Делать агрегацию на стороне финстаты, отдавать результаты в стриме <br/>
   В кликхаусе нет стриминга результата. Т.е на стороне финстаты всё равно нужно делать запросы
   с LIMIT OFFSET и превращать их в стрим. Это было бы сложно на стороне финстаты.
4. Выгружать большое кол-во данных не из clickhouse, а из yt.<br/>
   Нужно поддерживать консистентными 2 хранилища данных. Плюс нужно одинаково поддерживать
   логику - фильтры и прочее, для того и другого. Плюс само по себе начать использовать yt в сервисе
   финстаты, это не дешёвая задача.
5. Выгружать большое кол-во данных не из clickhouse, а из yt. Не из финстаты, а сразу сервисом команды потребителей.<br/>
   Размазывать логику между сервисами, которые будут в ответственности разных команд - интуитивно плохая идея.
   Проблемы аналогичные предыдущему варианту, ещё и на 2 команды.
6. Добавить ещё одно хранилище, возможно реляционную базу, которая хорошо справляется с подобными запросами.<br/>
   Аналогично предыдущим пунктам. Плюс эти данные понадобится как-то наливать в реляционную базу. Брокер сейчас такое не умеет,
   нужно будет писать своими силами и гарантировать записть. Или договариваться с брокером.

## Consequences
Мы выбрали апи(постранично выгружать из агрегатов) и имплементацию.
Имплементацию в будущем можно будет изменить.

### Good
Не дорого сделать. Если будет работать под нагрузкой, решение всех устраивает.

### Bad
Для кликхауса это не профильная нагрузка. Возможно в конечном итоге он не будет справляться
и понадобится выбрать и реализовать другой вариант.