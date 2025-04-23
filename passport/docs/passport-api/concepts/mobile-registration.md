# Регистрация в мобильном приложении

Минималистичная регистрация пользователей на мобильных телефонах. Создается особый «телефонный» аккаунт, который может авторизоваться только по OAuth-токену соответствующего мобильного приложения.

С таким аккаунтом невозможно авторизоваться на портале, и доступ к нему нельзя восстановить. В отличие от [веб-регистрации](web-registration-alt.md), пользователь только подтверждает номер телефона.

Чтобы авторизовать приложения по OAuth-токенам, отправьте [заявку](http://wiki.yandex-team.ru/oauth/newservice) на рассылку [oauth@](mailto:oauth@yandex-team.ru). OAuth-приложения регистрируйте на oauth.yandex.ru в [ обычном порядке](http://api.yandex.ru/oauth/doc/dg/tasks/register-client.xml).


## Шаги сценария {#prepare}

Чтобы зарегистрировать аккаунт, нужно только подтвердить номер телефона пользователя.

1. {% include [steps-create-track](../_includes/concepts/web-registration-phone/id-steps/create-track.md) %}
    
1. [Передайте в статистику](https://wiki.yandex-team.ru/passport/python/api/bundle/sysandstat#zapislogovdljastatistiki) данные о начале регистрации, перечисленные [на вики](https://wiki.yandex-team.ru/passport/statbox/#processregistraciina/1/account/register/phonish/).
    
1. {% include [step2-check-phone](../_includes/concepts/retail-registration/id-step2/check-phone.md) %}
    
    {% include [steps-valid-phone](../_includes/concepts/web-registration-phone/id-steps/valid-phone.md) %}
    
    Все отправленные поля формы (в том числе с невалидными значениями), [записывайте в статистику](https://wiki.yandex-team.ru/passport/python/api/bundle/sysandstat#zapislogovdljastatistiki) согласно [регламенту](https://wiki.yandex-team.ru/passport/statbox#processregistraciina/1/account/register/phonish/).
    
1. {% include [steps-phone-limits](../_includes/concepts/web-registration-phone/id-steps/phone-limits.md) %}
    
1. {% include [steps-phone-send](../_includes/concepts/web-registration-phone/id-steps/phone-send.md) %}
    
1. {% include [steps-phone-check](../_includes/concepts/web-registration-phone/id-steps/phone-check.md) %}
    
1. [Создайте аккаунт](https://wiki.yandex-team.ru/passport/python/api/bundle/registration#registracijaphonishakkaunta).
    
1. [Получите OAuth-токен](https://wiki.yandex-team.ru/passport/python/api/bundle/registration#sozdanietokena) для вашего приложения, передав в Паспорт данные приложения и идентификатор трека. Подробнее о токенах для мобильных приложений читайте [на вики-странице](https://wiki.yandex-team.ru/YandexMobile/server/OAuth#kakrabotaetaccountmanager).
    
1. {% include [steps-delete-track](../_includes/concepts/web-registration-phone/id-steps/delete-track.md) %}
    

