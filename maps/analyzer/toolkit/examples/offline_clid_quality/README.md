## Сравнение кач-ва пробок с пробочным партнёром и без него

Пример, который сравнивает качество прогноза ETA по пробкам в некотором регионе с учётом партнёра (`clid`) и без него, для этого:
1. Фильтрует пробочные проезды по региону и исключает из них исследуемый `clid`
2. Если партнёр сейчас отключён, то может заматчить его сигналы и добавить в пробочные проезды (опция `--match`)
3. Строит пробки без учёта партнёра и с ним
4. Берёт асессоров в нужном регионе, исключает из них исследуемый `clid`
5. Считает качество на асессорах на разных пробках

### TODO

* `join_travel_times` умеет переприклеивать пробки к training tracks, соот-но можно научить принимать и training tracks (там есть, например, fixprice); но нужно учесть, что они порёберные
* общие пробки хранятся какое-то время, их можно брать оттуда, а не строить заново; но тут нужно учесть, что в зависимости от включённости партнёра пробки могут означать как пробки с партнёром, так и без него
* training tracks имеет уже приклеенные пробки, соот-но достаточно просто пофильтровать по региону, но тут есть та же проблема, что и в пункте про использование готовых пробок
