# Модуль "Темы"

## Как работает ротация скинов

Логика ротации находится в моделе. Модель контроллирует когда и какой скин поставить.

Видам надо забирать `.currentSkin` и делать необходимые действия (поставить класс на html или обновить текст).
Т.о. вид должен всегда инвалидироваться при изменении модели.
 
Типичные действия:

**смена класс на html**

```js
ns.View.define('rotate-html-class', {
    events: {
        'ns-view-show': 'onShow'
    },
    
    models: {
        // вид должен инвалидироваться при изменении модели
        'theme-MySuperTheme': 'invalidate'
    },

    methods: {

        onShow: function() {
            // При каждой инвалидации будет вызываться onShow.
            // Берем текущий скин (.currentSkin) и ставим новый класс на html
            
            var mTheme = this.getThemeModel();
            var newSkin = mTheme.get('.currentSkin');

            this.updateSkinClass(newSkin);
        }
    }
};
```

**смена текста при ротации скина**

```js
// В этом случае вид получается минимальным
ns.View.define('rotate-footer-text', {
    models: {
        // вид должен инвалидироваться при изменении модели
        'theme-MySuperTheme': 'invalidate'
    }
});
```

```
// Отрисовываем текст для текущего скина
match .rotate-footer-text ns-view-content {
    skinInfo = ns-model-call('theme-MySuperTheme', 'getSkinText')
    skinInfo.text
}
```
