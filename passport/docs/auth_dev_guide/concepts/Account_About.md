# Учетная запись

Учетная запись (аккаунт) — это уникальный набор данных, соответствующих определенному пользователю Яндекса.

Уникальность обеспечивается UID — уникальным числовым идентификатором. UID присваивается каждому новому аккаунту на основе инкрементируемого счетчика регистраций и, таким образом, не используется повторно.

UID всегда соответствует той учетной записи, которой был назначен при регистрации. В качестве идентификатора рекомендуется использовать именно UID пользователя, так как логина у пользователя может не быть (например — [социальные](#social-user) и [телефонные](#phonish-user) аккаунты). Также логин пользователя может быть привязан к другому UID, если предыдущий аккаунт с таким логином был удален.

{% note info %}

UID не связан со значением куки `yandexuid`. Кука используется в статистике как идентификатор браузера и генерируется независимо от идентификаторов учетных записей.

{% endnote %}


Учетная запись содержит доступную пользовательскую информацию и персональные настройки: например, имя и фамилию, номер мобильного телефона, язык интерфейса и т. п. Наиболее востребованные данные учетных записей, которые хранит Паспорт, описаны в разделе [Часто используемые данные системы авторизации](DB_About.md).

Доступные пользователю способы авторизации зависят от атрибутов учетной записи, которые создал пользователь. Пользователи могут авторизоваться, используя следующие атрибуты:

- Логин и пароль.

    Обязательно задаются при стандартной регистрации в Паспорте ([ register](https://doc.yandex-team.ru/Passport/passport-modes/reference/register.html)) и при регистрации пользователей посредством API ([admimportreg](https://doc.yandex-team.ru/Passport/passport-modes/reference/admimportreg.html) для портальных сервисов, [mdapi](https://doc.yandex-team.ru/blackbox/concepts/about.xml) — для ПДД).

    Аккаунты ПДД и Моего Круга вместо логина используют e-mail.

- Социальный профиль.

    Данные об аккаунте пользователя в одной из поддерживаемых соцсетей (Twitter, Facebook, Вконтакте, Одноклассники, Mail.ru или Google). Пользователь может разрешить авторизацию с помощью социального профиля на странице [social.yandex.ru](https://social.yandex.ru). Подробнее о такой авторизации читайте в разделе [Социальный профиль](accounts-attributes.md#social-profile).

- Телефонный номер.

    Пользователи могут авторизовываться в мобильных приложениях при помощи телефонного номера. В этом случае подтверждением для входа является код, отправляемый пользователю в СМС-сообщении.


## Типы учетных записей {#section_lry_jnq_pcb}

Типы учетных записей определяются алиасами. Список типов аккаунтов расширяется и в актуальном виде существует в разделе [Типы алиасов](DB_About.md#aliases) или на [Вики](https://wiki.yandex-team.ru/passport/dbmoving/#tipyaliasov). Одной учетной записи (UID) может соответствовать несколько алиасов.

Основными типами учетных записей являются:

- Portal — основной тип учетной записи, <q>логин на Яндексе</q>. Пользователи с такими учетными записями прошли стандартную регистрацию в Паспорте, имеют логин и пароль.

    В отдельных случаях у таких аккаунтов может не быть почтового ящика (если он был удален пользователем) или адрес почтового ящика может не совпадать с логином пользователя.

- PDD — аккаунты пользователей Почты Для Домена. Такие аккаунты всегда имеют почтовый адрес в рамках своего домена. Аккаунты создаются администраторами доменов.

- Lite — пользователи без почтового ящика на Яндекс.Почте. Для входа используют электронный адрес на стороннем сервисе.

- Social — аккаунты, созданные при авторизации через одну из социальных сетей. Такие аккаунты не имеют логина и пароля, но впоследствии могут быть дорегестрированы до стандартных аккаунтов Яндекса. Вход в учетную запись Яндекса подтверждается на сайте социальной сети.

- Phonish — аккаунты, созданные при авторизации по номеру мобильного телефона. Такие аккаунты создаются без логина и пароля и имеют проблемы, связанные с переходим телефонного номера от одного владельца к другому.


Алиасам аккаунтов соответствуют свои подписки (SID). Подробнее о подписках см. раздел [Подписка на сервис (SID)](SID_About.md). Все существующие алиасы и соответствующие им SID приведены в таблице [Типы алиасов](DB_About.md#aliases).

