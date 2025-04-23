#image-preview#

##Описание##
Создаёт превью изображения, при клике на которое оригинал изображения будет показан в модальном окне.
Может создавать превью в двух режимах:
1. На основе url превью, переданного в параметрах
2. Масштабированием: на основе оригинальной картинки и парраметра scale

###Автор###
[evolkowa](https://staff.yandex-team.ru/evolkowa)

##Примеры##
1. Формирование превью на основе url превью в параметрах
{
    block: 'image-preview',
    previewUrl: 'https://im2-tub-ru.yandex.net/i?id=305a200f16e16a10a39026383196e271&n=33&h=215&w=225',
    imageUrl: 'http://www.youloveit.ru/uploads/posts/2016-02/1455101714_1439646049_youloveit_ru_zootopia_shakira.jpg'
}

2. Формирование превью масштабированием: на основе оригинальной картинки и параметра scale
{
    block: 'image-preview',
    imageUrl: 'http://cs5.pikabu.ru/images/previews_comm/2015-12_5/1450692509125147471.png',
    width: 400,
    height: 321,
    scale: 0.5,
    hintContent:[
        {
            elem: 'hint-icon',
            content: '!!!'
        },
        'Сделать побольше'
    ]
}

