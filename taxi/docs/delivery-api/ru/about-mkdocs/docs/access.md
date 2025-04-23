# Как получить доступ к API

## Боевой доступ {#prod-access}

Все запросы к API Яндекс&#160;Доставки в&#160;другой день выполняются к хосту `https://b2b-authproxy.taxi.yandex.net`.

Пример запроса к боевому хосту: `https://b2b-authproxy.taxi.yandex.net/api/b2b/platform/offers/create`.

{% note info "Внимание." %}

Bearer-токен нужно получить в [личном кабинете](https://dostavka.yandex.ru/account) (раздел «Профиль»).

Bearer-токен действует неограниченное время. Но если вы поменяете пароль от [Кабинета Корпоративного Клиента](https://dostavka.yandex.ru/login/), ваш Bearer-токен перестанет действовать, его нужно будет получить повторно.

{% endnote %}

Используйте Bearer-токен во всех запросах. Передавайте токен в заголовке `Authorization`:

```html
Authorization: Bearer <OAuth-токен>
```

## Тестовый доступ {#test-access}

Все запросы к API Яндекс&#160;Доставки в&#160;другой день выполняются к хосту `https://b2b.taxi.tst.yandex.net/`.

Пример запроса к тестовому хосту: `https://b2b.taxi.tst.yandex.net/api/b2b/platform/offers/create`.

Используйте следующий Bearer-токен для тестовых запросов: `AgAAAADzeAQMAAAPeISvM_9LUkxCijQoFXOH5QE`.

Используйте следующий `platform_station_id` для тестовых запросов: `7c4054cd-d768-4062-8f8d-d0c9b3c8c4e8`.


## Получение OAuth-токена {#get-oauth-token}

1. Войдите в [Кабинет Корпоративного Клиента](https://dostavka.yandex.ru/login/) с помощью выданного вам логина и пароля.

1. Перейдите на вкладку [Профиль компании](https://dostavka.yandex.ru/login/profile/settings/).

1. В разделе **Токен для API** нажмите **Получить**.

1. На странице [https://oauth.yandex.ru](https://oauth.yandex.ru) нажмите **Разрешить**.

1. В Кабинете Корпоративного Клиента Яндекс&#160;Доставки на вкладке **Профиль компании** в разделе **Токен для API** будет отображен ваш OAuth-токен.

1. Создайте заявку и отслеживайте состояние заказа с помощью API в соответствии с порядком обработки заявки.


## Остались вопросы? {#questions}

Ответы на часто задаваемые вопросы собраны в [соответствующем разделе](https://yandex.ru/dev/logistics/delivery-api/doc/faq/faq.html).

По всем вопросам, связанными с интеграцией, методами и работой API Яндекс&#160;Доставки в&#160;другой день, вы можете [обратиться в поддержку](https://yandex.ru/dev/logistics/delivery-api/doc/troubleshooting/troubleshooting.html).
