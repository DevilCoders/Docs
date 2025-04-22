# b-feature-marker-popup

Содержимое попапа с заданным сообщением и кнопками "Понятно" и "Подробнее".

При нажатии на любую из кнопок генерируется событие `'hide'` c параметром `isDetails` (нажатая кнопка является кнопкой "подробнее"). 

[внешний вид](https://jing.yandex-team.ru/files/dima117a/Redaktirovanie_gruppy_objyavlenii_2017-11-23_13-25-18.png)

## Пример

```js
{
    block: 'b-feature-marker-popup',
    text: 'текст сообщения',
    helpUrl: 'https://yandex.ru'    // ссылка для кнопки "подробнее"
}
```
