# Сущность "Brand"

Объект содержащий данные об одном отдельном бренде на Маркете.

### Поля:
  - **id** `<Integer>` - идентификатор бренда в Маркете
  - **name** `<String>` - название бренда
  - description `<String>` - краткое описание бренда
  - country `<String>` - страна производства бренда
  - site `<String>` - URL сайта бренда
  - foundationYear `<Number>` - год основания бренда
  - recommendedShopsUrl `<String>` - URL страницы рекомендованых магазинов
  - descriptionSource [`<HtmlLink>`] - ссылка на полное описание бренда
  - logo [`<Image>`] - логотип бренда
  - picture [`<Image>`] - большое изображение бренда (на данный момент там всегда полноразмерный логотип)
  - ~~logoUrl~~ `<String>` - _(deprecated)_ URL адрес логотипа (только в случае если присутствует логотип, и если он представлен УРЛом)

Жирным указаны поля, обязательно присутствующие, при получении сущности с бекенда.

### Примечания
  - Поле `logoUrl` оставлено для обратной совместимости, если оно присутствует, то его значение гарантированно равно значению поля `logo.url`. После внесённых изменений, бекенд может присылать логотип бренда и другие изображения в одном из двух вариантов (см. описание сущности [`<Image>`](/_entities/Image.md)). Так что поле `logoUrl` будет присутствовать **только** если в бренде так же присутствует поле `logo`, и **только** если в поле `logo` присутствует поле `url`. В дальнейшем это поле будет удалено.
  - Поле `foundationYear` должно быть натуральным числом в диапазоне от 1000 до 9999.

### Примеры:
```
{
  "id": 42,
  "name": "Hysteric Glamour",
  "description": "Hysteric Glamour is a Japanese designer label created by artist Nobuhiko Kitamura in 1984",
  "country": "Japan",
  "site": "http://www.hystericglamour.jp/",
  "descriptionSource": {
    "url": "http://www.hystericglamour.jp/brand/",
    "text": "Сайт производителя"
  },
  "logo": {
    "url": "http://i.imgur.com/Kt6lt6y.jpg"
  },
  "picture": {
    "url": "http://i.imgur.com/9Ek5wnm.jpg"
  },
  "logoUrl": "http://i.imgur.com/Kt6lt6y.jpg"
}
```
```
{
  "id": 42,
  "name": "Golden Gaytime",
  "description": "Golden Gaytime (Cookie Crumble in New Zealand) is a popular ice cream snack, made and distributed by the Streets confectionery company in Australia, and first released in 1959.",
  "country": "New Zealand",
  "site": "http://www.streetsicecream.com.au/Brand/Golden_Gaytime.aspx",
  "logo": {
    "body": "iVBORw0KGgoAAAANSUhEUgAAAGAAAA==",
    "type": "png"
  }
}
```

[`<HtmlLink>`]: /_entities/HtmlLink.md
[`<Image>`]: /_entities/Image.md