# @yandex-int/hermione-block-diff-comparison-plugin

Плагин для выборочного игнорирования диффов в assertView.

Использование:

hermione.conf.js
```(js)
{
    ...
    plugins: {
        ...
        '@yandex-int/hermione-block-diff-comparison-plugin': {
            enabled: true,
            size: {
                width: '<int>',
                height: '<int>'
            },
            restrictions: {
                maxBlockSize: '<int>',
                maxDiffPixelsRatio: '<float 0-1>'
            }
        }
    }
}
```

`width` и `height` это ширина и высота скриншота (нужны для `maxDiffPixelsRatio`)

`maxBlockSize` размер "квадрата" участка диффа, который будет считаться настоящим диффом. Например `maxBlockSize: 3` будет считать, что если на картинке есть сплошной блок диффов, размером 3х3 пикселя — это фейл. Все блоки диффа 2х2, 2х1, 3х1, etc он будет игнорировать.

`maxDiffPixelsRatio` соотношение диффа к исходному скриншоту. Например `maxDiffPixelsRatio: 0.1` будет значить, что считаем сравнение скриншотов фейлом только если > 10% пикселей отличаются.
