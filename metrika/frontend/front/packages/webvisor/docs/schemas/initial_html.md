Структура данных HTML (отправляется при первом запуске Recorder'a)

```javascript
{
  // Группа событий (фиксированное значение)
  // Необходимо для сборки событий на уровне плеера
  group: 'page',

  // Детальная информация о странице
  meta: {
    doctype   : String  // Доктайп страницы
    title     : String  // Заголовок страницы
    address   : String  // Полный адрес страницы
    ua        : String  // UserAgent
    referrer  : String  // Реферер, если есть
    base      : String  // location.href или значение атрибута href тега base
    hasBase   : Boolean // был ли на странице тег base изначально или нам надо добавлять его при проигрываниии

    // Размеры экрана
    screen    : Object({
      width     : Number
      height    : Number
    })

    // Размеры вьюпорта с учетом текущего зума страницы
    viewport: Object({
      width     : Number
      height    : Number
    })

    // Детальный разбор адреса страницы
    location: Object({
      host      : String
      protocol  : String
      path      : String
    })

    // Ненулевые значения скролла для всех элементов страницы
    initialScroll: Array<Object({
      target    : Number
      scroll    : Array[Number, Number]
    })>
  },

  // Это самый главный объект, в нем содержится JSON-интерпретация
  // DOM дерева по которой в дальнейшем оно будет воспроизводиться
  // в плеере, менять структуру или убирать ее нельзя
  content: Object
}
```
