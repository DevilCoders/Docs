# pager

Навигационный элемент для перемещения по страницам.
 
## Элементы
### `home-button`
Кнопка, которая отображается перед пейджером и ведет на первую страницу.

## Поля
### `withArrows`
Флаг, который указывает на то, что слева и справа допустимых страниц будут навигационные стрелки.

### `totalPages`
Количество всех страниц.

### `currentPage`
Текущая страница.

### `visible`
Количество видимых кнопок в блоке.

### `queryParam`
Префикс, который будет меняться в урле каждой страницы. По умолчанию `page`.

### `url`
Стартовый урл.
 
-----------------------------

Пример использования:
 
``` js
{
    block: 'pager',
    withArrows: true,
    totalPages: 123,
    currentPage: 2,
    visible: 5,
    queryParam: 'page',
    url: '%%%basePath%%%/search/?',
    content: currentPage > 1 ? {
        elem: 'home-button',
        text: this.i18n('pager', 'to-the-begining') // В начало
    } : ''
}
```

