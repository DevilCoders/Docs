# Resizer
Библиотека для работы с Ресайзером (https://wiki.yandex-team.ru/Resizer)



##`createToken`

Создает подписанный URL картинки

#### Arguments
1. `url` *(String)*
2. `width` *(Number)*: ширина результирующего изображения
3. `height` *(Number)*: высота результирующего изображения
4. `otherParams` *(Object|String)*: дополнительные параметры или typemap

   `otherParams.typemap` *(String)*

   `otherParams.crop = 0` *(Number)*

   `otherParams.enlarge = 0` *(Number)*

   `otherParams.goldenratio = 1` *(Number)*

##### Returns
*(String)*
#### Example
```js
Resizer.createToken(
    'http://avatars.mds.yandex.net/get-itunes-icon/24055/325a89ad48b458c44421b0a27dfa28af/orig', 44, 44,
    {
        typemap: 'gif:gif;png:png;*:jpeg;',
        crop: 0,
        goldenratio: 1
    }
)
/*
    '//resize.yandex.net/0e5e61f83baf8d15d9ae28cafab87b95?'
        + 'key=e204623661add00ae8f6aa69d0e8866d&'
        + 'url=http%3A%2F%2Favatars.mds.yandex.net%2Fget-itunes-icon%2F24055%2F325a89ad48b458c44421b0a27dfa28af%2Forig&'
        + 'width=44&'
        + 'height=44&'
        + 'typemap=gif%3Agif%3Bpng%3Apng%3B*%3Ajpeg%3B&'
        + 'crop=no&'
        + 'enlarge=no&'
        + 'goldenratio=no'
*/
```


* * *
