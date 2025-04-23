# Веб-регистрация с номером телефона

В этом сценарии, по сравнению с [базовой веб-регистрацией](web-registration-alt.md), пользователь теряет возможность задать контрольный вопрос, но обязательно должен подтвердить номер телефона. Получая грант на весь сценарий, вы автоматически получаете гранты на каждый вызов, предусмотренный сценарием.

Грант запрашивайте на [passport-admin@](passport-admin@yandex-team.ru) для сценария`phonereg`.

{% note info %}

Яндекс.Почта использует вариацию сценария `phonereg` — `digitsreg`. С точки зрения пользователя различие между ними состоит только в том, что в сценарии `digitsreg` для зарегистрированного пользователя автоматически включается [номер телефона вместо логина](http://help.yandex.ru/passport/authorization/phone-login.xml).

Также для `digitsreg` записывается гораздо больше событий статистики, все они перечислены [на вики](https://wiki.yandex-team.ru/passport/statbox#processregistraciimodedigitsreg/1/account/register/phoneandaliasify/).

{% endnote %}



## Шаги сценария {#steps}

### Подготовка регистрации {#prepare}

Перед тем как предлагать пользователю вводить данные, подготовьтесь к регистрации.

1. [Создайте трек](https://wiki.yandex-team.ru/passport/python/api/bundle/track#sozdattrek) (серверный контейнер для данных о конкретной регистрации).
    
1. Проверьте, выставлена ли кука `yandexuid`. Если у пользователя нет такой куки, ее нужно выставить по [правилам](https://wiki.yandex-team.ru/Cookies/yandexuid/).
    
1. [Передайте в статистику](https://wiki.yandex-team.ru/passport/python/api/bundle/sysandstat#zapislogovdljastatistiki) данные о начале регистрации, перечисленные [на вики](https://wiki.yandex-team.ru/passport/statbox/#processregistraciimodephonereg/1/account/register/phone/).
1. Если после регистрации пользователь должен перейти по определенному адресу («retpath»), [проверьте этот адрес](https://wiki.yandex-team.ru/passport/python/api/bundle/validate#proveritadresobratnogoredirektaretpath). Неизвестный или некорректный адрес замените редиректом по умолчанию — на [https://passport.yandex.ru/passport?mode=passport](https://passport.yandex.ru/passport?mode=passport).
    
1. Определите [язык](https://wiki.yandex-team.ru/passport/python/api/bundle/suggest#opredelitjazyk) и [страну](https://wiki.yandex-team.ru/passport/python/api/bundle/suggest#opredelitstranu) пользователя.
    
1. [Запишите данные](https://wiki.yandex-team.ru/passport/python/api/bundle/track#zapisatvtrek) о начале регистрации в трек: язык, страну, URL редиректа после регистрации, а также укажите источник регистрации (идентификатор сервиса и, опционально, конкретной акции продвижения).
    

### Обработка пользовательского ввода {#input}

С помощью API Паспорта вы можете помочь пользователю ввести нужные данные, а также отсеять роботов.

- Для имени и фамилии можно предоставлять одно поле, а введенную строку [разделять на составляющие](https://wiki.yandex-team.ru/passport/python/api/bundle/suggest#vydelitimjaifamilijuizodnojjstroki).
    
- Пол пользователя можно [определить по имени и фамилии](https://wiki.yandex-team.ru/passport/python/api/bundle/suggest#opredelitpolpoimeniifamilii).
    
- Часовой пояс пользователя можно [определить по IP клиента](https://wiki.yandex-team.ru/passport/python/api/bundle/suggest#opredelitchasovojjpojas).
    
- Текстовые поля формы проверяйте соответствующими методами API:
    
    - Для логина [проверяйте](https://wiki.yandex-team.ru/passport/python/api/bundle/validate#proveritlogin) доступен ли он, содержит ли стоп-слова или запрещенные символы.
    
    - Для пароля [проверяйте](https://wiki.yandex-team.ru/passport/python/api/bundle/validate#proveritparol) его сложность, длину и наличие запрещенных символов.
    
    - Телефонный номер, введенный пользователем, можно [привести](https://wiki.yandex-team.ru/passport/python/api/bundle/validate#proverittelefonnyjjnomerikonvertirovategovmezhdunarodnyjjformat) к международному формату.
    
- Если пользователь выбрал уже занятый логин или не указал его совсем, предложите ему [список свободных логинов](https://wiki.yandex-team.ru/passport/python/api/bundle/suggest#predlozhitspisokloginov).
    

По мере того, как пользователь заполняет форму, в трек нужно записывать следующие данные:

- флаг различия пароля при первом и втором (проверочном) вводе;
    
- UNIX-время второго ввода пароля;
    
- общее количество изменений пароля после подсказки о том, что пароль слабый.
    

Все отправленные поля формы (в том числе с невалидными значениями), [записывайте в статистику](https://wiki.yandex-team.ru/passport/python/api/bundle/sysandstat#zapislogovdljastatistiki) по [инструкции](https://wiki.yandex-team.ru/passport/statbox/#processregistraciimodephonereg/1/account/register/phone/) для данного сценария.

### Подтверждение номера телефона {#phone-confirm}

Чтобы пользователь мог подтвердить номер телефона:

1. Проверьте [ограничения](https://wiki.yandex-team.ru/passport/python/api/bundle/phone#proveritogranichenijaischetchikisms) на отправку SMS для этого номера.
    
1. [Отправьте SMS с кодом](https://wiki.yandex-team.ru/passport/python/api/bundle/phone/#/submit). В ответе Паспорт возвращает время, когда сообщение можно будет выслать заново (например, если SMS не дошло до пользователя).
    
1. [Проверьте введенный код](https://wiki.yandex-team.ru/passport/python/api/bundle/phone/#/commit).
    

### Завершение регистрации {#finish}

Паспорт создает новый аккаунт, и пользователя можно авторизовать под созданным логином.

1. [Создайте аккаунт с привязанным телефоном](https://wiki.yandex-team.ru/passport/python/api/bundle/registration#registracijaakkauntapriobjazatelnomnalichiiprovalidirovannogotelefona), передав Паспорту все данные, которые были собраны о пользователе.
    
1. [Авторизуйте пользователя](https://wiki.yandex-team.ru/passport/python/api/bundle/registration#sozdaniesessii) и сразу [проверьте](https://wiki.yandex-team.ru/passport/python/api/bundle/registration#proverkaustanovlennojjsessii)выставленные авторизационные куки.
    
1. [Удалите трек регистрации](https://wiki.yandex-team.ru/passport/python/api/bundle/track#udalittrek) в Паспорте.
    
1. Перенаправьте пользователя на страницу, которую он должен увидеть после регистрации.

