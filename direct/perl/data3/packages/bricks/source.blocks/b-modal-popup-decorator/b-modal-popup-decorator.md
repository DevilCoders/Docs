#b-modal-popup-decorator#

##Описание##
Блок-декоратор модального попапа. Отрисовывает попап с набором дефолтных модификаторов, помещает внутри него
заданный блок с контентом. Блок с контентом должен имплементировать интерфейс `i-modal-popup-inner-block-interface`.
Блок умеет блокировать закрытие в случае наличия изменений во внутреннем блоке контента попапа, подстраивать высоту
попапа при появлении скроллбара. Модальные попапы созданные с помощью этого блока имеют общий внешний вид, подробнее
[тут](https://st.yandex-team.ru/DIRECT-49241#1450720310000)

###Меинтейнеры###
[ngraf](https://staff.yandex-team.ru/ngraf)

##Пример##
```javascript
    BEM.DOM.decl({ block: 'b-block-popup-content', implements: 'i-modal-popup-inner-block-interface' }, {

        onSetMod: {
            js: function() {
                var buttons = this.findBlocksInside('button');

                buttons[0].on('click', function() {
                    this.findBlockInside('input').val('');

                    this.trigger('save');
                }, this);

                buttons[1].on('click', function() {
                    this.trigger('cancel');
                }, this);
            }
        },

        /**
         * Были ли изменения
         * @returns {$.Deferred<Boolean>}
         */
        isChanged: function() {
            var deferred = $.Deferred();

            deferred.resolve(!u._.isEmpty(this.findBlockInside('input').val()));

            return deferred;
        }

    });

    var modal = BEM.DOM.blocks['b-modal-popup-decorator'].create();

    modal
        .on('close-blocked', function() {
            var popup = modal.getPopup();

            BEM.DOM.blocks['b-confirm'].open({
                title: iget('Есть несохранённые изменения'),
                question: iget('Вы действительно хотите закрыть?'),
                message: [],
                fromPopup: popup,
                onYes: function() {
                    modal.hide({ force: true });
                }
            });
        })
        .on('close', function() {
            modal.destruct();
        });

    modal
        .setPopupContent({
            block: 'b-block-popup-content',
            content: [
                {
                    elem: 'header',
                    mix: { block: 'b-modal-popup-decorator', elem: 'header' },
                    content: 'Header on the top (as is w/o font-size)'
                },
                {
                    elem: 'body',
                    mix: { block: 'b-modal-popup-decorator', elem: 'body' },
                    content: [
                        'Body under the footer and below the header (surprise!)<br />',
                        {
                            block: 'input',
                            mods: { size: 'xs' },
                            content: { elem: 'control' }
                        }
                    ]
                },
                {
                    elem: 'footer',
                    mix: { block: 'b-modal-popup-decorator', elem: 'footer' },
                    content: [
                        { block: 'button', mods: { theme: 'normal', size: 'xs' }, content: iget('OK') },
                        '&nbsp;',
                        { block: 'button', mods: { theme: 'normal', size: 'xs' }, content: iget('Отмена') },
                        '&nbsp;Footer here, let\'s place here some info'
                    ]
                }
            ]
        })
        .on('save cancel', function() {
            modal.hide();
        });

    modal.show();
```
