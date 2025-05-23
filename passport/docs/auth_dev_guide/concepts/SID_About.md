# Подписка на сервис (SID)

Подписка — это способ формальной классификации учетных записей с помощью определенных атрибутов. Чаще всего подписки используются для идентификации пользователей определенного сервиса.

Подписки позволяют:

- Специальным образом реагировать на удаление аккаунтов (например, запрещать удаление учетных записей с нерешенными денежными вопросами).
- Оформлять отказ пользователей от сервиса. Например, удаление почтового ящика с точки зрения системы авторизации — это отмена подписки на Почту. Отмена подписки отражается в базе `historydb` (база содержит историю всех операций над аккаунтами).
- Отображать ссылку на сервис в меню стандартной шапки Лего, выпадающем при нажатии на имя пользователя.

Для оформления подписки необходим SID (Service ID) — идентификатор, который объединяет определенный срез пользователей. (Например, SID 2 — это идентификатор Почты, а SID 67 указывает на пользователей с ужесточенными требованиями к паролю.)

Также SID необходим, чтобы идентифицировать сервис при взаимодейтсвии с Паспортом.

## Подписка на SID {#subscribe}

В процессе подписки учетной записи присваивается SUID (Service UID); наличие SUID равнозначно подписке на сервис. Проверить наличие SUID можно, запросив поле [`suid`](DB_About.md#suid) с помощью Черного ящика.

{% note info %}

Пара SUID/SID используется для идентификации учетных записей только Почтой и Народом. Для прочих сервисов SUID в рамках SID могут не быть уникальными, идентифицировать аккаунты следует с помощью UID.

{% endnote %}


## Получение SID {#howto}

SID заводится командой Паспорта по запросу сервиса. Запрос следует оформить в задаче [проекта Паспорта](https://jira.yandex-team.ru/browse/PASSP), либо в письме на рассылку [passport-dev@](mailto:passport-dev@yandex-team.ru).

#### Данные, необходимые для запроса SID

- URL и название сервиса.
- Менеджер проекта (контактное лицо).
- Короткое имя сервиса для идентификации в Паспорте (например, `mail`).
- URL для редиректа пользователей после регистрации.
- URL для редиректа пользователей после авторизации.
- Название сервиса в шапке регистрации (например, «Видео»).
- Необходимость отображать сервис в выпадающем меню имени пользователя, реализованном в шапке Лего.

    Если сервис должен быть включен в меню, нужно предоставить также URL локализированных сервисов для всех нужных языков и переводы названия.

- Текст ссылки на сервис, которую нужно предлагать пользователям после регистрации.
- Политика отмены подписки на сервис. Например, подписка на Директ не может быть удалена, если у пользователя есть активные рекламные кампании.

- Текст предупреждения о последствиях отмены подписки. Например: «При удалении почтового ящика восстановить письма будет невозможно».
- Способ подписки на SID. Возможно три варианта:

    - подписывать на SID не планируется (если SID создается только для бронирования короткого названия или для мимикрии);
    - подписка через браузер (с помощью режима [`subscribe`](https://doc.yandex-team.ru/Passport/passport-modes/reference/subscribe.html));
    - подписка серверным вызовом (с помощью режима [`admsubscribe`](https://doc.yandex-team.ru/Passport/passport-modes/reference/admsubscribe.html)).

    Подписка через браузер позволяет подписаться на SID просто перейдя на соответствующий URL. Чтобы контролировать каждую подписку, следует разрешить и использовать только серверные вызовы.

Получив заявку, команда Паспорта заводит SID и вносит его в [список имеющихся SID](http://wiki.yandex-team.ru/passport/SIDs). После этого разработчики сервиса могут:

- Подписывать пользователей на сервис.
- Идентифицировать подписанных пользователей.
- Регистрировать новые учетные записи от лица сервиса, направляя их на режим Паспорта [`register`](https://doc.yandex-team.ru/Passport/passport-modes/reference/register.html) с нужными параметрами. Если для SID настроена мимикрия, стандартное оформление регистрации будет изменено.

