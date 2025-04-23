# CSS

Похоже на BEM, но не BEM. Элементы можно вкладывать внутрь других элементов.
Используем нейминг:

```css
blockBlock-elementElement_modifier
```

Например:

```css
.head
.head-inner
.head-inner_messages
.head-inner_compose
```

## Разные особенности
* в CSS при использовании ```transform: translate()``` надо всегда дописывать ```translateZ(0)```. Это надо из-за того, что:
  * ```translateZ``` включает аппаратное ускорение
  * iScroll ставит ```translateZ```, а если его где-то не будет, то он сбрасывается и страница начинает мигать при анимации
* в CSS при использовании ```transform: translate()``` обязательно надо выставлять начальный `transform: translate(0, 0) translateZ(0)`, иначе можно словить интересные артефакты
