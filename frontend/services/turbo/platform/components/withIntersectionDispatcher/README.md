## withIntersectionDispatcher(keyName?: string)

Записывает в `store` видимость элемента во *viewport* браузера.
HOC передает в  `props` оборачиваемого компонента функцию`onIntersectionChange: (isInViewport: boolean) => void`, которая должна вызваться при изменении видимости элемента во *viewport* браузера.

В `store` добавляется объект, у которого в качестве ключей используется `id` элемента, или, при отсутствии `id`, параметр функции `keyName?: string`.

```
isInViewport: {
	[id || keyName]: true | false
}
```

`true` - часть элемента находится во *viewport*
`false` - элемент полностью вне *viewport*
