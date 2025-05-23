# Отзыв токенов

Яндекс.OAuth отзывает токены в следующих случаях:

- Токен был отозван пользователем на странице [Доступ внешних приложений]{% if lang == "ru" %}(https://passport.yandex.ru/profile/access){% endif %}{% if lang == "en" %}(https://passport.yandex.com/profile/access){% endif %}. При отзыве OAuth-токена соответствующий refresh-токен отзывается автоматически.

- Срок жизни токена истек.

- Владелец приложения изменил запрашиваемые права либо удалил приложение. В этом случае отзываются все токены, когда-либо выданные этому приложению.

- Пользователь совершил действие, при котором отзываются все OAuth-токены и refresh-токены, когда-либо выданные для учетной записи:

  - изменил пароль;
  
  - включил или выключил [двухфакторную аутентификацию]{% if lang == "ru" %}(https://help.yandex.ru/passport/authorization/twofa.xml){% endif %}{% if lang == "en" %}(https://help.yandex.com/passport/authorization/twofa.xml){% endif %};
  
  - успешно восстановил доступ к аккаунту;
  
  - перешел по ссылке **Выйти на всех компьютерах** в [Яндекс ID]{% if lang == "ru" %}(https://passport.yandex.ru/passport?mode=passport){% endif %}{% if lang == "en" %}(https://passport.yandex.com/passport?mode=passport){% endif %} или на каком-то другом сервисе.

## Отзыв токенов в приложении {#token-revocation}

Приложение может отзывать OAuth-токены, которые были [выданы для определенного устройства](../concepts/device-token.md), с помощью специального запроса к {{ service }}.

Чтобы реализовать выход из учетной записи для обычных токенов, можно удалять соответствующие ей токены из локального хранилища — восстановить удаленный токен через {{ service }} невозможно, приложение должно будет запросить доступ заново.

При этом для пользователя на странице [Доступ внешних приложений]{% if lang == "ru" %}(https://passport.yandex.ru/profile/access){% endif %}{% if lang == "en" %}(https://passport.yandex.com/profile/access){% endif %} ничего не изменится. Токен, выданный приложению, будет считаться активным, пока не будет отозван каким-либо из перечисленных выше способом.
