# Моды

https://st.yandex-team.ru/TAXIPROJECTS-825

## Проблемы

### Black и схожие с ним

* Надо выделять тарифы в группу со своим отображением
* Различное особое поведение в моде (не показывать эконом точки в моде black, например)

### Беспилотник и схожие с ним

* Поведение забито только для беспилотника, хотя оно схоже для других идей, например для лодок
* Много описаний в конфигах разбросано
* Непонятно как исключать из списка тарифов те, которые в моде беспилотника

## Преложения

* Расширить описание мод тем, как отображать разные элементы
* Добавить возможность переходить в моду по выбору тарифа
* Унифицровать моды с переходом по точке из зоны

## MVP

### zoneinfo

в supported добавляем флажок

#### не поддерживает моды

* не возвращать тарифы из моды с переходом по зоне
* все остальные тарифы возвращать с модой default для текущих клиентов

#### поддерживает моды

* вернуть тарифы с их модами as is
* в описание мод добавить описание интерфейсов и плашки для перехода в мод, если есть

### persuggest

* не ломаться от неизвестных мод
* убрать зашитые значения
* решить вопрос с модами и коддиспатчем

### routestats

* получаем выбранную моду
* возвращаем мультикласс для каждой моды

### конфиги

Расширить описание мод