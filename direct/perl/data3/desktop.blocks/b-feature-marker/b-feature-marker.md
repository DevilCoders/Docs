# b-feature-marker

Блок `b-feature-marker` примешивается к другому блоку и отображает возле его DOM элемента [нестандартный попап](https://jing.yandex-team.ru/files/dima117a/Redaktirovanie_gruppy_objyavlenii_2017-11-23_13-25-18.png), обращающий на себя внимание.
После закрытия попапа устанавливается cookie и при последующем открытии страницы попап не отображается.

## Пример

```js
{
    block: 'b-any-block',
    mix: {
        block: 'b-feature-marker',
        js: {
            featureId: 'autotargeting',
            helpUrl: u.getCommonHelpUrl('/direct/features/autotargeting.html'),
            text: iget2('b-any-block', 'xxx', 'Пример текста.')
        }
    }
}
```
