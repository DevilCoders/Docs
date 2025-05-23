# Библиотека для выполнения групповых операций над геообъектами

Библиотека позволяет
* загружать из БД объекты в пределах заданной области с заданным фильтром
* изменять геометрию объектов
* изменять атрибуты объектов
* изменять связи между объектами

## Особенности реализации

Загрузка из БД происходит пачками в главном потоке.
На каждый загруженный объект вызывается лямбда-обработчик в отдельном потоке.
Использовать одно и то же соединение к БД одновременно в обоих потоках нельзя.

## Расширения

Поверх библиотеки были реализованы операции более высокого уровня:
* Подвижка по спутнику `actions/move.h`
* Задание или удаление атрибутов группе объектов `actions/update_attrs.h`
* Удаление объектов в области с учётом связей `actions/delete.h`
