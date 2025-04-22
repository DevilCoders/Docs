#b-banner-all-formats

##Описание
Показывает все варианты отображения объявления в сети (по табам).
В `previews` передается массив с описанием табов, где в `name` название элемента
блока `b-banner-all-formats`, а в `data` - данные которые будут пробросаны в элемент

###Автор 
[grimfrid](https://staff.yandex-team.ru/grimfrid )

###Где используется
`i-banner-all-formats-opener`
   
###Взаимодействие с другими блоками
Получает данные из `i-banner-all-formats-opener`

##Пример##

```
{
    block: 'b-banner-all-formats',
    active: 'context',
    previews: [
        { name: 'context', data: {} },
        { name: 'video', data: {} },
    ]
}

```
