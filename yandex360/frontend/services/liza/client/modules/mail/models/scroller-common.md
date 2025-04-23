# Модель-скроллер

Цели этой модели:
 1. Определять scroll-area для видов
 2. Инкапсулировать логику рассчета свойств scroll-area (для window и обычных нод они немного разные)
 3. Иметь единственный правильный обработчик скролла, который делает `throttle`, кеширует свойства и т.п.
 
Все это позволяет избежать дублирования код в видах.

## API

```
ns.View.define('my-view', {

    events: {
        'ns-view-show': 'onShow',

        'daria:vScrollerMessages:scroll@show: 'onScroll'
    },

    models: {
        'scroller-messages': false
    },

    methods: {

        onShow: function() {
            // инициализацию придется делать в ручную,
            // потому что в момент создания модели ноды-скроллера в 3pane может не быть
            this.getModel('scroller-messages').init();
        },

        // никакого debounce/throlle/timeout делать не надо, они идет из коробки
        onScroll: function() {
            var mScroller = this.getModel('scroller-messages');

            if (mScroller.getScrollTop() < 100) {
                this.loadMessagesOnScroll()
            }
        }
    }
}
```

Модели кидают глобальные события, чтобы вьюха могла отписаться от него при скрытии:
 * `daria:vScrollerMessage:scroll` - скролл области письма
 * `daria:vScrollerMessages:scroll` - скролл области списка писем

С обработчиком события не надо ничего делать дополнительно, правильный троттлинг делает сама модель. 

## Кто есть кто

 * `scroller-message` - модель скроллера письма/треда (правая колонка в 3pane)
 * `scroller-messages` - модель скроллера списка писем (средняя колонка в 3pane)

Какую модель использовать лучше всего определять по тому, где находится твой вид в 3pane.
