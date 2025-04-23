# Веб-регистрация с телефоном или контрольным вопросом

Сценарий базовой веб-регистрации: пользователь может подтвердить номер телефона или задать ответ на контрольный вопрос. Получая грант на весь сценарий, вы автоматически получаете гранты на каждый вызов, предусмотренный сценарием.

Грант запрашивайте на [passport-admin@](passport-admin@yandex-team.ru) для сценария`alternative`.


## Шаги сценария {#steps}

### Подготовка регистрации {#prepare}

{% include [steps-prepare-intro](../_includes/concepts/web-registration-phone/id-steps/prepare-intro.md) %}


1. {% include [steps-create-track](../_includes/concepts/web-registration-phone/id-steps/create-track.md) %}
    
1. {% include [steps-yandexuid](../_includes/concepts/web-registration-phone/id-steps/yandexuid.md) %}
    
1. [Передайте в статистику](https://wiki.yandex-team.ru/passport/python/api/bundle/sysandstat#zapislogovdljastatistiki) данные о начале регистрации, перечисленные [на вики](https://wiki.yandex-team.ru/passport/statbox/#processregistraciina/1/account/register/alternative/).
    
1. {% include [steps-retpath](../_includes/concepts/web-registration-phone/id-steps/retpath.md) %}
    
1. {% include [steps-lang-country](../_includes/concepts/web-registration-phone/id-steps/lang-country.md) %}
    

### Обработка пользовательского ввода {#input}

{% include [steps-process-intro](../_includes/concepts/web-registration-phone/id-steps/process-intro.md) %}


- {% include [steps-sex-suggest](../_includes/concepts/web-registration-phone/id-steps/sex-suggest.md) %}
    
- {% include [steps-valid-intro](../_includes/concepts/web-registration-phone/id-steps/valid-intro.md) %}
    
    - {% include [steps-valid-login](../_includes/concepts/web-registration-phone/id-steps/valid-login.md) %}
    
    - {% include [steps-valid-pass](../_includes/concepts/web-registration-phone/id-steps/valid-pass.md) %}
    
    - {% include [steps-valid-phone](../_includes/concepts/web-registration-phone/id-steps/valid-phone.md) %}
    
- {% include [steps-login-suggest](../_includes/concepts/web-registration-phone/id-steps/login-suggest.md) %}
    
- Для пользователей, которые регистрируются с контрольным вопросом (без номера телефона), [сгенерируйте](https://wiki.yandex-team.ru/passport/python/api/bundle/captcha/#generacijanovojjkapchi) и покажите капчу. [Проверьте](https://wiki.yandex-team.ru/passport/python/api/bundle/captcha/#proverkakapchi) введенное значение.
    

{% include [steps-write-track-input](../_includes/concepts/web-registration-phone/id-steps/write-track-input.md) %}


- {% include [steps-track-input-diverge](../_includes/concepts/web-registration-phone/id-steps/track-input-diverge.md) %}
    
- UNIX-время второго ввода пароля, а также UNIX-время ввода контрольного вопроса и ответа;
    
- {% include [steps-track-input-mesh](../_includes/concepts/web-registration-phone/id-steps/track-input-mesh.md) %}
    

### Подтверждение номера телефона {#phone-confirm}

{% include [steps-phone-confirm-intro](../_includes/concepts/web-registration-phone/id-steps/phone-confirm-intro.md) %}


1. Проверьте [ограничения](https://wiki.yandex-team.ru/passport/python/api/bundle/phone#proveritogranichenijaischetchikisms) на отправку SMS для этого номера.
    
1. [Отправьте SMS с кодом](https://wiki.yandex-team.ru/passport/python/api/bundle/phone/#/submit). В ответе Паспорт возвращает время, когда сообщение можно будет выслать заново (например, если SMS не дошло до пользователя).
    
1. [Проверьте введенный код](https://wiki.yandex-team.ru/passport/python/api/bundle/phone/#/commit).
    

### Завершение регистрации {#finish}

{% include [steps-end-intro](../_includes/concepts/web-registration-phone/id-steps/end-intro.md) %}


1. {% include [steps-create-account](../_includes/concepts/web-registration-phone/id-steps/create-account.md) %}
    
1. {% include [steps-authorize](../_includes/concepts/web-registration-phone/id-steps/authorize.md) %}
    
1. {% include [steps-delete-track](../_includes/concepts/web-registration-phone/id-steps/delete-track.md) %}
    

