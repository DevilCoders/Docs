# native-scroll

Блок `native-scroll` предназначен для создания прокрутки различного контента по горизонтали. Реализован на основе нативного элемента, имеющего горизонтальную прокрутку, у которого скрываются полосы прокрутки.

Сейчас блок выполнен только в CSS. В дальнейшем планируется расширить функциональность JS-методами для управления его поведением.  

При использовании блока ему необходимо указать фиксированную высоту в CSS.

```js
{
    block: 'native-scroll',
    attrs: {style: 'height: 30px; width: 100%;'},
    content: {
        tag: 'span',
        attrs: {style: 'white-space: nowrap; line-height: 30px'},
        content: 'Scroll me >>> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris a nisl ' +
            'mattis tellus tempor ultrices vitae sed arcu. Aliquam eget magna orci. Aliquam ' +
            'blandit sapien sed enim malesuada, eu ullamcorper augue blandit. Phasellus ut lorem ' +
            'ut augue cursus sodales. Proin ultricies dictum pulvinar. Donec ut ligula id metus ' +
            'lacinia vehicula vitae vitae felis. Proin eleifend odio ac lorem sodales, vel porta ' +
            'risus accumsan. Phasellus eget quam tortor. Donec congue turpis ac lacus feugiat laoreet. ' +
            'Suspendisse et lobortis metus, at bibendum nunc. Nunc tincidunt elit eleifend ' +
            'odio tincidunt egestas. Ut condimentum tempus augue, vitae porttitor nisi scelerisque ' +
            'sed. Sed rutrum tellus mauris, vitae dapibus purus ullamcorper non. Nam quis est vel erat ' +
            'ullamcorper posuere. Praesent adipiscing malesuada vehicula. Proin non ' +
            'vulputate arcu. Aliquam convallis bibendum semper. Nulla accumsan interdum ' +
            'augue, in ullamcorper ante posuere vitae.'
    }
}
```
