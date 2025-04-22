# Протокол OAuth 2.0

Протокол OAuth 2.0 позволяет приложениям работать с сервисами Яндекса от имени пользователя. Доступ каждого приложения явно ограничивается правами, заданными при его регистрации. О базовых принципах OAuth, а также об особенностях протокола в Яндексе читайте раздел [{#T}](ya-oauth-intro.md).

OAuth-авторизацию поддерживают [Диск]{% if lang == "ru" %}(https://tech.yandex.ru/disk/){% endif %}{% if lang == "en" %}(https://tech.yandex.com/disk/){% endif %}, [Вебмастер]{% if lang == "ru" %}(https://tech.yandex.ru/webmaster/){% endif %}{% if lang == "en" %}(https://tech.yandex.com/webmaster/){% endif %}, [Метрика]{% if lang == "ru" %}(https://tech.yandex.ru/metrika/){% endif %}{% if lang == "en" %}(https://tech.yandex.com/metrika/){% endif %} и другие сервисы.

## Как воспользоваться OAuth {#how-to-use}

Чтобы начать пользоваться протоколом, необходимо:

1. [Зарегистрировать](../tasks/register-client.md) приложение на {{ service }}.
    
1. Реализовать получение токена одним из двух способов:
    
    - Извлечь токен из хэша URL (часть адреса после символа #).
    
      Способ описан в инструкциях для [мобильных](../reference/mobile-client.md), [настольных](../reference/desktop-client.md) и [веб-приложений](../reference/web-client.md).
    
    - Запросить токен в обмен на код подтверждения. С помощью кода подтверждения можно решать проблемы не приспособленных для URL приложений:
    
      - Если важно получить токен в теле ответа, а не в URL, — запросите [код, который можно обменять на токен](../reference/auto-code-client.md).
      - Если в приложении сложно получить доступ к URL редиректа, вы можете запросить [вывод кода для пользователя на Яндекс.OAuth](../reference/console-client.md).
      - Если на устройстве сложно вводить код, можно [попросить пользователя ввести код на Яндекс.OAuth](../reference/simple-input-client.md).
    
{% if audience == "internal" %}

{% note info %}

Для сервисов и приложений Яндекса доступны [дополнительные способы](../reference/resource-owner-credentials.md) получения OAuth-токенов.

{% endnote %}

{% endif %}

Тестировать OAuth-приложения можно с помощью [отладочных токенов](../tasks/get-oauth-token.md).
