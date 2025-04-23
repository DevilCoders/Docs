# Введение

API Яндекс&#160;Доставки предоставляет корпоративным клиентам возможность использовать HTTP-запросы для заказа доставки отправлений.

Вы можете сделать заказ экспресс-доставки на ближайшее время, то есть начать поиск исполнителя сразу после подтверждения заявки, или сделать отложенный заказ — задать желаемые параметры приезда курьера на точку А. 
Также можно воспользоваться доставкой в течение дня, доставка будет осуществляться в выбранные часовые интервалы.

Перед началом работы с API [получите OAuth-токен](access.md).

Создайте заявку и отслеживайте состояние заказа с помощью API в соответствии с [порядком обработки заявки](claim-process.md).

В случае возникновения каких-либо проблем свяжитесь с вашим менеджером Яндекс&#160;Доставки.

## Материалы для интеграции {#integration}

Если вы пользуетесь сторонним программным обеспечением для интеграции с сервисами Яндекс&#160;Доставки, познакомьтесь, пожалуйста, с нашими [примерами интеграции](https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/api/files/Yandex_Delivery_Express_API_postman_collection-ru.zip), выполненными в программе Postman. Вы можете скачать файл и использовать его для отладки и редактирования запросов.

В меню коллекции добавьте свой [OAuth-токен](access.md). После этого вы сможете протестировать все добавленные запросы и при необходимости сгенерировать готовый код на самых распространенных языках программирования.

<a class="doc-c doc-c-button doc-c-button_theme_action doc-c-button_size_m doc-c-button_js_inited" href="https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/api/files/Express_RU.pdf"><span class="doc-c-button__text">Гайд для «Экспресс-доставки»</span></a>&#160;<a class="doc-c doc-c-button doc-c-button_theme_action doc-c-button_size_m doc-c-button_js_inited" href="https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/api/files/SDD_RU.pdf"><span class="doc-c-button__text">Гайд для «Доставки в течение дня»</span></a>

<a class="doc-c doc-c-button doc-c-button_theme_action doc-c-button_size_m doc-c-button_js_inited" href="https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/api/files/Yandex_Delivery_Express_API_postman_collection-ru.zip"><span class="doc-c-button__text">Готовые примеры интеграции Postman</span></a>