# Двухэтапная регистрация для ритейлеров

Некоторые мобильные приложения Яндекса предустанавливаются на телефоны, продаваемые в розницу. Многие предустанавливаемые приложения (Почта, Диск и т. д.) предполагают, что у пользователя есть аккаунт Яндекса. Чтобы пользователю не приходилось проходить весь процесс регистрации, можно использовать двухэтапный сценарий:

1. Сотрудник магазина создает аккаунт с логином, который выбрал пользователь. На телефоне сохраняется OAuth-токен, с которым пользователь сможет авторизоваться для активации аккаунта.
1. Пользователь активирует аккаунт: задает пароль и подтверждает номер телефона.

К июлю 2014 года сценарий был реализован [группой разработки App Store](https://staff.yandex-team.ru/departments/yandex_distproducts_browserdev_mobile_appstore/).


## Создание аккаунта {#step1}

Пользователь сообщает сотруднику магазина свое имя, фамилию и желаемый логин на Яндексе. Сотрудник вводит полученные данные в специальной программе, предоставленной Яндексом. В этой программе следует реализовать следующую последовательность вызовов:

1. {% include [steps-create-track](../_includes/concepts/web-registration-phone/id-steps/create-track.md) %}
    
1. [Проверьте логин](https://wiki.yandex-team.ru/passport/python/api/bundle/validate#proveritlogin). Если запрошенный логин занят, можно предложить [список альтернатив](https://wiki.yandex-team.ru/passport/python/api/bundle/suggest#predlozhitspisokloginov).
    
    Все отправленные поля формы (в том числе с невалидными значениями), [записывайте в статистику](https://wiki.yandex-team.ru/passport/python/api/bundle/sysandstat#zapislogovdljastatistiki) по [инструкции](https://wiki.yandex-team.ru/passport/statbox#processregistraciimoderegisterbymiddleman/1/account/register/bymiddleman/) для данного сценария.
    
1. Определите пол, язык и страну пользователя.
    
    - {% include [steps-sex-suggest](../_includes/concepts/web-registration-phone/id-steps/sex-suggest.md) %}
    
    - Язык и страну можно найти в системных настройках телефона. Если найти не удалось, следует считать их русскими по умолчанию.
    
1. [Создайте аккаунт](https://wiki.yandex-team.ru/passport/python/api/bundle/registration#registracijanezavershennogopolzovatelja). Если Паспорт отвечает, что нужна проверка капчей, [сгенерируйте](https://wiki.yandex-team.ru/passport/python/api/bundle/captcha/#generacijanovojjkapchi) и покажите капчу. [Проверьте](https://wiki.yandex-team.ru/passport/python/api/bundle/captcha/#proverkakapchi) введенное значение.
1. [Удалите трек](https://wiki.yandex-team.ru/passport/python/api/bundle/track#udalittrek), чтобы завершить создание аккаунта.
    


## Активация аккаунта {#step2}

Получив телефон, пользователь может активировать созданный аккаунта через приложение Яндекса. Для этого приложение должно реализовать следующую последовательность вызовов:

1. [Создайте трек](https://wiki.yandex-team.ru/passport/python/api/bundle/track#sozdattrek) по OAuth-токену, полученному после первого этапа.
1. Получите номер телефона от пользователя.
    
    {% include [steps-valid-phone](../_includes/concepts/web-registration-phone/id-steps/valid-phone.md) %}
    
1. {% include [steps-phone-send](../_includes/concepts/web-registration-phone/id-steps/phone-send.md) %}
    
1. {% include [steps-phone-check](../_includes/concepts/web-registration-phone/id-steps/phone-check.md) %}
    
1. Получите пароль от пользователя, [проверьте](https://wiki.yandex-team.ru/passport/python/api/bundle/validate#proveritparol) сложность и состав пароля.
1. [Установите пароль](https://wiki.yandex-team.ru/passport/python/api/bundle/registration#prostanovkaparolja) для аккаунта.
1. {% include [prepare-get-x-token](../_includes/concepts/mobile-registration/id-prepare/get-x-token.md) %}
    
1. {% include [steps-delete-track](../_includes/concepts/web-registration-phone/id-steps/delete-track.md) %}
    

{% note warning %}

{% include [step1-submit-stat](../_includes/concepts/retail-registration/id-step1/submit-stat.md) %}

{% endnote %}


