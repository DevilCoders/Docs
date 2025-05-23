## Вызовите функцию {#invoke}

{% note info %}

Чтобы любой пользователь мог вызывать функцию, необходимо [сделать ее публичной](../../functions/operations/function-public.md). Подробнее о правах читайте в разделе [{#T}](../../functions/security/index.md).

{% endnote %}

{% list tabs %}

- Консоль управления

    1. В [консоли управления]({{ link-console-main }}) перейдите в каталог, в котором находится функция.
    1. Выберите сервис **{{ sf-name }}**.
    1. Выберите функцию.
    1. Перейдите на вкладку **Тестирование**.
    1. В поле **Тег версии** укажите ```$latest```, чтобы вызвать последнюю версию функции.
    1. В поле **Шаблон данных** выберите **Без шаблона**.
    1. Нажмите кнопку **Запустить тест**.
    1. В разделе **Результат тестирования**, в поле **Состояние функции**, будет показан статус тестирования. **Важно**: максимальное время выполнения функции до [таймаута](../../functions/operations/function/version-manage.md#version-create) (включая начальную инициализацию при первом запуске) — 10 минут.
    1. В поле **Ответ функции** появится результат выполнения функции.

- CLI

    {% include [cli-install](../cli-install.md) %}

    {% include [default-catalogue](../default-catalogue.md) %}

    Чтобы вызвать функцию, выполните команду:

    ```
    yc serverless function invoke <идентификатор функции>
    ```

    По умолчанию вызывается версия функции с тегом `$latest`.


- HTTPS

	Ссылку для вызова функции можно найти на вкладке **Обзор**, в поле **Ссылка для вызова**.

	Для обеспечения безопасности функцию можно вызвать только по протоколу HTTPS. Вызовите ее как обычный HTTPS-запрос, вставив ссылку в адресную строку браузера:

	```
	{{ sf-url }}/b09bhaokchn9pnbrlseb
	```

	На странице появится ответ:

	```
	Hello, World!
	```

- Yandex Cloud Toolkit

    Вызвать функцию можно с помощью [плагина Yandex Cloud Toolkit]{% if lang == "ru" %}(https://github.com/yandex-cloud/ide-plugin-jetbrains){% endif %}{% if lang == "en" %}(https://github.com/yandex-cloud/ide-plugin-jetbrains/blob/master/README.en.md){% endif %} для семейства IDE на [платформе IntelliJ]{% if lang == "ru" %}(https://www.jetbrains.com/ru-ru/opensource/idea/){% endif %}{% if lang == "en" %}(https://www.jetbrains.com/opensource/idea/){% endif %} от [JetBrains](https://www.jetbrains.com/).

{% endlist %}