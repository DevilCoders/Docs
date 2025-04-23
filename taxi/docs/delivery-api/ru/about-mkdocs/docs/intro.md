# Введение

API Яндекс Доставки в другой день предоставляет возможность сделать заказ в другой день при помощи HTTP-запросов, а именно воспользоваться доставкой с классическим забором с вашего склада и доставкой до конечного получателя. Кроме того, возможен самопривоз товара в определенные точки отгрузки и доставка до ПВЗ.

![Схема](https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/delivery-api/files/scheme-0.png)

Перед началом работы с API получите Bearer-токен в [личном кабинете](https://dostavka.yandex.ru/account) (раздел «Профиль») или воспользуйтесь тестовым токеном  `AgAAAADzeAQMAAAPeISvM_9LUkxCijQoFXOH5QE` и тестовым хостом [https://b2b.taxi.tst.yandex.net/api/b2b/platform/offers/create](https://b2b.taxi.tst.yandex.net/api/b2b/platform/offers/create).

При запросе в боевую среду воспользуйтесь хостом [https://b2b-authproxy.taxi.yandex.net](https://b2b-authproxy.taxi.yandex.net) и боевой станцией `platform_station_id`.

Создайте заявку и отслеживайте состояние заказа с помощью API в соответствии со [статусной моделью](status-model.md).

В случае возникновения каких-либо проблем свяжитесь с вашим менеджером Яндекс Доставки или со [службой поддержки](https://yandex.ru/dev/logistics/delivery-api/doc/troubleshooting/troubleshooting.html).

## Материалы для интеграции {#integration}

Если вы пользуетесь сторонним программным обеспечением для интеграции с сервисами Яндекс Доставки, ознакомьтесь, пожалуйста, с нашими [примерами интеграции](https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/delivery-api/files/YandexDeliveryNDDAPI_postman_collection_ru.zip), выполненными в программе Postman. Вы можете скачать файл и использовать его для отладки и редактирования запросов.

По нажатии на коллекцию добавьте свой Bearer-токен (токен с префиксом `Bearer`). После этого вы сможете протестировать все добавленные запросы и при необходимости сгенерировать готовый код на самых распространенных языках программирования.

<a class="doc-c doc-c-button doc-c-button_theme_action doc-c-button_size_m doc-c-button_js_inited doc-c-link doc-c-link_type_external doc-c-i-bem doc-c-link_js_inited" href="https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/delivery-api/files/NDD_RU.pdf" target="_blank"><span class="doc-c-button__text">Гайд для «Доставки в другой день»</span></a>

<a class="doc-c doc-c-button doc-c-button_theme_action doc-c-button_size_m doc-c-button_js_inited doc-c-link doc-c-link_type_external doc-c-i-bem doc-c-link_js_inited" href="https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/delivery-api/files/YandexDeliveryNDDAPI_postman_collection_ru.zip" target="_blank"><span class="doc-c-button__text">Готовые примеры интеграции Postman</span></a>
