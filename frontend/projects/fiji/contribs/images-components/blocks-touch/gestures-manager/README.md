# gestures-manager

Блок по управлению жестами на контейнере.


Для использования:
1. Примиксовать блок gesture-manager на какой-либо элемент с вашим блоком:
```js
{
    block: 'someBlock',
    mix: [{ block: 'gestures-manager' }]
}
```
2. Добавить вашему блоку в зависимости `gestures-manager` и необходимые жесты, которые реализованы в блоке `gesture` и различаются модификатором `type`:
```js
[{
    shouldDeps: [
        { block: 'gesture', mods: { type: ['tap', 'pan', 'pinch'] } },
        { block: 'gestures-manager' }
    ]
}];
```
3. В клиентском .js своего блока, найти экземпляр `gestures-manager`:
```js
this._gesturesManager = this.findBlockOn('gestures-manager');
```

4. В найденный экземпляр передать контейнер и экземпляры требуемых жестов, после чего подписать на события:

```js
// Устанавливаем контейнер и жесты
this._gesturesManager
    .setContainer(this.elem('image-container'))
    .setGestures([
        BEM.create({ block: 'gesture', mods: { type: 'pinch' } }),
        BEM.create({ block: 'gesture', mods: { type: 'tap' } }),
        BEM.create({ block: 'gesture', mods: { type: 'pan' } })
    ]);
// Подписываемся на события
this._gesturesManager.on({
    'pinchstart pinch': this._onPinch,
    'panstart pan': this._onPan,
    pinchend: this._onPinchEnd,
    panend: this._onPanEnd,
    doubletap: this._onDoubleTap,
    tap: this._onSingleTap
}, this);
```

5. В обработчиках событий реализовать необходимое вам поведение.
