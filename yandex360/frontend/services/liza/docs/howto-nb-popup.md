# Динамическое создание попапов

Правильным путем создание и показа попапа является его генерация on-demand, т.е. по клику.
Это удобнее, потому что попап не надо обновлять при изменении данных, он открывается сразу акрутальным.
И это быстрее, потому он создает и ренедрится, когда действительно необходим


Вот так должен выглядеть элемент, который открывает попап
```js
/**
 * @class Daria.vSimplePopupToggler
 * @augments ns.View
 */
ns.View.define('simple-popup-toggler', {
    events: {
        'click': 'openPopup'
    },

    yateModule: 'toolbar',

    /** @lends Daria.vSimplePopupToggler.prototype */
    methods: {

        openPopup: function() {
            // Если попап открыт, то второй клик его закрывает
            // Если попап был закрыт по внешнему клику, то он будет невалидным и мы его пересоздадим
            if (this.vPopup && this.vPopup.isValid()) {
                this.vPopup.close();
                this.vPopup = null;
                return;
            }

            this.vPopup = ns.View.create('layout-switch-popup');
            this.vPopup.open({
                where: this.$node
            });
        }
    }
});
```

Вот так должен выглядеть сам попап
```js
/**
 * @class Daria.vSimplePopup
 * @augments ns.View
 */
ns.View.define('simple-popup', {

    yateModule: 'toolbar',

    /** @lends Daria.vSimplePopup.prototype */
    methods: {

        /**
         * Открывает попап
         * @param {object} options Опции для nbPopup.open()
         */
        open: function(options) {
            this.update({}, { execFlag: ns.U.EXEC.PARALLEL }).then(function() {

                this.nbPopup = nb.block(this.node);
                this.nbPopup.open(options);

                // уничтожаем себя при закрытии
                this.nbPopup.on('nb-closed', this.destroySelf.bind(this));
            }, this);
        },

        /**
         * Закрывает попап
         */
        close: function() {
            if (this.nbPopup) {
                this.nbPopup.close();
            }
        },

        destroySelf: function() {
            var that = this;
            // попап может находится в синхронном процессе скрытия
            // делаем _.defer, чтобы он завершил процесс
            _.defer(function() {
                // уничтожаем попап
                if (that.nbPopup) {
                    that.nbPopup.destroy();
                    that.nbPopup = null;
                }

                // уничтожаем себя
                that.destroy();
            });
        }

    }
});
```

```yate
match .simple-popup ns-build-view {
    nb-popup({
        'attrs': {
            'data-key': '{ /.key }'
        }
        'class': [
            'ns-view-{ /.id }'
            /.uniqueId
        ]
        'content': (
            apply . ns-build-view-content
        )
    })
}

match .simple-popup ns-view-content {
    // содержимое попапа
}
```
