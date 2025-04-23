Блок для отображения кнопок-действий с продуктами и сокращателя ссылок для страницы.

=== Параметры bemjson
- actions [array] Список возможных действий, например [{type: 'add', url: '#'}]

==== type: add
Отображает и передает параметры в блок b-modal-trigger
- {string} url Ссылка для блока b-modal-trigger
- {string} [text] Content для кнопки блока b-modal-trigger, по умолчанию - BEM.I18N('b-products-actions', 'Add')
- {string} [popupType] Тип попапа блока b-modal-trigger, по умолчанию - pi
