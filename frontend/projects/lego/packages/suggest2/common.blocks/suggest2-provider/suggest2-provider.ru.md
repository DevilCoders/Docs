# suggest2-provider

Вспомогательный блок `suggest2-provider` — это провайдер данных. Он предоставляет данные о подсказках [саджеста](../suggest2/suggest2.ru.md) посредством AJAX-запросов. Позволяет настраивать запросы к серверу с данными через [JS-параметры](../suggest2/suggest2.ru.md#js-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D0%B1%D0%BB%D0%BE%D0%BA%D0%B0)  блока `suggest2`.

Схема получения данных с сервера:

![Схема](http://www.plantuml.com/plantuml/img/NOux4i8m34Hxdq8NeA5qmI6uWOWrnamY6rdAS7piaC-GJjhLwYsQPhRfGU8AYgOX5MI5QZ5IrQjBN4pXSeCf1nez34_aI6xPkbmapocGU11wMukuJUbk9PcxXo_yx0S_yHok9NEbl_IAp7nVNMZmCBQgEtxhwK4bjL6EJry0)

| Модификатор                | Допустимые значения | Способы установки | Описание                             |
| -------------------------- | --------------------| ------------------| ------------------------------------ |
| [undo](#mods-undo)         | `yes`               | JS                | Исправляет поведение отмены ввода    |
