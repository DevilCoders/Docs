### Общие элементы блока данных о пользователе

#### address-list
Список e-mail адресов пользователя. Черный ящик составляет список в зависимости от значения [аргумента emails](../../concepts/emails.md), если аргумент не передан, список адресов не возвращается. Список может быть пустым.

#### address-list->address
e-mail адрес пользователя из запрошенного списка.

#### address-list->born-date
Дата и время внесения электронного адреса в список e-mail пользователя, в формате YYYY-MM-DD HH:MM:SS.<br/><br/>Для внутренних e-mail это дата и время регистрации аккаунта. Для внешних e-mail это дата и время, когда адрес был добавлен пользователем.

#### address-list->default
Признак того, что e-mail является адресом по-умолчанию.<br/><br/>Если в запросе был передан параметр `emails=getdefault`, это будет единственным адресом в списке.<br/> Если у пользователя есть хотя бы один подтвержденный e-mail адрес, то среди них всегда будет адрес по-умолчанию. У пользователя может не быть ни одного подтвержденного адреса и тогда адреса по-умолчанию тоже не будет.

#### address-list->native
Признак внутреннего e-mail, т.е. ящика на Яндексе, принадлежащего текущему аккаунту. Обычно логинная часть адреса совпадает с логином пользователя, но полагаться на это нельзя, т.к. возможны исключения. <br/> Внутренних адресов может не быть, например, если у пользователя нет почтового ящика или почтовый ящик заморожен.

#### address-list->rpop
Признак почтового ящика, письма с которого забирает почтовый сборщик Яндекса.<br/><br/>Т.к. письма из этого ящика автоматически собираются в основной ящик пользователя, такие e-mail-ы нельзя использовать для восстановления пароля.

#### address-list->native
Признак внутреннего e-mail, т.е. ящика на Яндексе, принадлежащего текущему аккаунту. Обычно логинная часть адреса совпадает с логином пользователя, но полагаться на это нельзя, т.к. возможны исключения. <br/> Внутренних адресов может не быть, например, если у пользователя нет почтового ящика или почтовый ящик заморожен.

#### address-list->rpop
Признак почтового ящика, письма с которого забирает почтовый сборщик Яндекса.<br/><br/>Т.к. письма из этого ящика автоматически собираются в основной ящик пользователя, такие e-mail-ы нельзя использовать для восстановления пароля.

#### address-list->silent
Признак адреса, на который не следует отправлять оповещения, новости и т.п. На такие адреса следует отправлять только критически важные письма.

#### address-list->unsafe
Признак адреса, который был подтвержден небезопасно.<br/><br/>Например, подтвержден через серверный вызов API Паспорта.<br/>Безопасным считается адрес добавленный непосредственно в интерфейсе Паспорта и подтвержденный вводом пароля. Такие адреса пригодны для восстановления доступа к аккаунту.

#### address-list->validated
Признак подтвержденности электронного адреса. E-mail считается подтвержденным, если пользователь доказал, что обладает доступом к нему, например, перейдя по ссылке из письма. Внутренние адреса, для которых выставлен атрибут `native`, так же считаются подтвержденными.

#### aliases
Список алиасов аккаунта. <br/><br/> В списке присутствуют только алиасы из параметра `aliases` исходного запроса, которые были найдены у аккаунта. Отсутствующие алиасы в список не включаются.<br/><br/> Полный список алиасов аккаунта приведен в [таблице алиасов](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#aliases)

#### attributes
Список атрибутов аккаунта. <br/><br/> В списке присутствуют только атрибуты из параметра `attributes` исходного запроса, которые были найдены у аккаунта. Отсутствующие атрибуты в список не включаются.<br/><br/> Полный список атрибутов аккаунта приведен в [таблице атрибутов](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#db-attributes)

#### dbfields
Значения атрибутов аккаунта в терминах полей старой базы данных Паспорта. <br/><br/> Устаревший способ получения данных о пользователе. Обращаться к базе данных рекомендуется с помощью параметра `attributes`.<br/><br/> В список включаются все имена полей, запрошенные в параметре `dbfields`. Если запрошенное значение поля неизвестно, значение соответствующего элемента возвращается пустым.

#### display_name
Содержит элементы с данными о визуальной идентификации пользователя на сервисах Яндекса: имя, аватар, используемый социальный профиль.<br/><br/>Возвращается, если в запросе задан параметр `regname`.

#### display_name->avatar
Свойства аватара пользователя.<br/><br/>Идентификатор аватара содержится во вложенном элементе `default`.<br/>Изображение для аватара можно скачать по ссылке следующего формата:<br/>`https://avatars.mds.yandex.net/get-yapic/<идентификатор аватара>/<размер>`<br/>Если аватара с переданным идентификатором нет, по ссылке будет заглушка нужного размера.<br/><br/>Доступные размеры, которые можно задать в URL аватара:<br/><br/>- `islands-small` — 28×28 пикселей.<br/>- `islands-34` — 34×34 пикселей.<br/>- `islands-middle` — 42×42 пикселей.<br/>- `islands-50` — 50×50 пикселей.<br/>- `islands-retina-small` — 56×56 пикселей.<br/>- `islands-68` — 68×68 пикселей.<br/>- `islands-75` — 75×75 пикселей.<br/>- `islands-retina-middle` — 84×84 пикселей.<br/>- `islands-retina-50` — 100×100 пикселей.<br/>- `islands-200` — 200×200 пикселей.<br/><br/>`empty` - Признак отсутствия аватара у пользователя. При этом в качестве идентификатора аватара в элементе `default` выдается идентификатор аватара по-умолчанию.

#### display_name->display_name_empty
Появляется в ответе при добавлении параметра [is_display_name_empty](#is_display_name_empty)

true - display_name вычислен на лету
false - display_name взят из базы

#### display_name->name
Имя, предназначенное для показа пользователю в интерфейсе. По-умолчанию это логин, введенный при регистрации. Для аккаунта, зарегистрированного через социальную сеть, используется имя, полученное от соцсети (имя и фамилия в Facebook, никнейм в Twitter и т.п.).<br/><br/>Пользователь может самостоятельно выбрать предпочтительное имя на странице [Выбор имени на Яндексе](https://passport.yandex.ru/profile/display-name).

#### display_name->public_name
Имя пользователя, предназначенное для показа в интерфейсе другим пользователям. Пользователь может выбрать себе публичное имя на странице [Выбор имени на Яндексе](https://passport.yandex.ru/profile/display-name).<br/><br/>Если публичное имя не настроено, но у пользователя указаны имя и фамилия, используется формат <q>имя + первая буква фамилии</q>. Например — <q>Иванов И.</q><br/><br/>Если ФИО отсутствует и публичное имя не настроено, используется логин или email пользователя, указанный при регистрации.

#### display_name->social->profile_id
Идентификатор социального профиля.

#### display_name->social->provider
Двухбуквенный код провайдера данных для социального профиля.<br/><br/>Список поддерживаемых провайдеров см. в вики: [https://wiki.yandex-team.ru/social/providers](https://wiki.yandex-team.ru/social/providers).

#### display_name->social->redirect_target
Токен, с помощью которого генерируется URL для перехода на публичную страницу пользователя на сайте провайдера.<br/><br/>Подробнее о ссылках на сайт провайдера см. вики: [https://wiki.yandex-team.ru/social/redirect](https://wiki.yandex-team.ru/social/redirect).

#### display_name->verified
Признак верифицированности пользователя: `true`, если признак есть. Если признака нет, то поле отсутсвует.
См. [пользовательский контент](../../concepts/ugc.md#verified).

#### emails
Данные о привязанных электронных адресах пользователя.<br/><br/>Возвращается, если в запросе задан параметр `getemails`.

#### email->id
Идентификатор электронного адреса пользователя.

#### email->attribute
Значение атрибута почтового адреса. Полный список атрибутов e-mail-ов приведен [в таблице атрибутов e-mail-ов](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#section_gyv_v5f_2hb).

#### family_info

Краткая информация о семье, в которой состоит пользователь. Появляется в ответе, если в запросе задан параметр [get_family_info](#get_family_info).

#### family_info->family_id

Идентификатор семьи. Получить более подробную информацию о ней можно в [method=family_info](../../methods/family_info.md).

#### family_info->admin_uid

UID админа семьи.

#### id
UID учетной записи, описанной в данном елементе `user`.<br/><br/> Появляется в ответе в тех случаях, когда выдаётся информация сразу о нескольких аккаунтах. Элемент позволяет идентифицировать к какому `uid` относится данный блок данных. В XML-ответе является свойством элемента `user`. <br/> В случае, если текущий элемент `user` относится к несуществующему аккаунту, или аккаунту, сессия которого не валидна, у него не будут заполнены другие элементы ответа, в том числе не будет заполнен элемент [`uid`](#uid). В таком случае элемент `id` позволяет однозначно идеоднозначно идентифицировать аккаунт, к которому относится данный блок.

#### karma
Карма пользователя — показатель того, что учетная запись подозревается в рассылке спама или была зарегистрирована автоматически (см. раздел [Карма](https://docs.yandex-team.ru/authdevguide/concepts/accounts-attributes#karma)).<br/><br/>Используемые значения:<br/>- 0 — пользователь не является спамером.<br/>- 80 — пользователь считался спамером по оценке старой версии Фродобороны. В настоящее время значение «80» пользователям не назначается.<br/>- 85 — пользователь с высокой вероятностью является спамером.<br/>- 100 — пользователь определенно является спамером.

#### karma->allow-until
UNIX-время, по наступлении которого сервису рекомендуется отказать пользователю в обслуживании. Вычисляется как сумма UNIX-времени выставления «плохой» кармы и случайного промежутка (в пределах нескольких часов). «Плохой» считается карма со значениями 85 и 100.<br/><br/>До указанного момента права пользователя нельзя ограничивать, основываясь только на значении кармы. Рекомендуется перепроверить карму непосредственно перед тем как отказать в обслуживании: сотрудники поддержки могут улучшить карму пользователя за прошедшее время.<br/><br/>Интерпретация «отказа в обслуживании» зависит от сервиса. Контентным сервисам (например, Фоткам) рекомендуется полностью блокировать учетную запись. Коммуникационным сервисам (например, Почте) рекомендуется отказывать пользователю в отдельных действиях (например, в отправке письма), показывая капчу или возвращая ошибку недоступности сервиса.<br/><br/>Атрибут используется для борьбы со скриптами автоматической регистрации. Блокируя пользователя через случайное время, сервис скрывает причину неудачи скрипта.<br/><br/>Таким образом, автору скрипта становится труднее диагностировать ошибки.

#### karma_status
Необработанная (сырая) карма — значение кармы, которое может содержать дополнительные данные об изменении кармы после регистрации.

#### login
Логин учетной записи на Яндексе.<br/><br/>Значение зависит от вида учетной записи:<br/>—  Для портального аккаунта — в точности тот логин, который был задан при регистрации. Т.е. значение не нормализовано и сохраняет регистр и позиции точек и дефисов. <br/>— Для ПДД и лайт-аккаунтов — e-mail, который используется для входа. <br/>— Для аккаунтов, не имеющих человекочитаемого логина, например, фониши или аккаунты, зарегистрированные через социальную сеть, поле содержит пустую строку. <br/><br/> Подробнее про типы учетных записей можно почитать [здесь](../../concepts/user-account.md#section_aliases)

#### phones
Данные о привязанных телефонных номерах пользователя.<br/><br/>Возвращается, если в запросе задан параметр `getphones`.

#### phone(s)->id
Идентификатор телефона пользователя.

#### phone(s)->attribute
Значение атрибута телефонного номера. Полный список атрибутов телефонов приведен [в таблице атрибутов телефонов](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#section_kbk_b5f_2hb).

#### plus_subscriber_state

Появляется в ответе, если в запросе был [параметр](#get_plus_subscriber_state).

[Подробное описание от команды Плюса](https://wiki.yandex-team.ru/plus/backend/blackbox-plus-subscriber-state/) (со всеми вопросами обращаться туда).

#### public_id
[Публичный идентификатор пользователя](../../concepts/ugc.md#public-id).<br/><br/>Возвращается, если в запросе задан параметр `get_public_id`.

#### regname
Устаревший элемент. Логин, введенный пользователем при регистрации, следует получать из элемента `login`. Имя для отображения в интерфейсе — из элемента `display_name`.<br/><br/>- Если пользователь регистрировался в Паспорте, элемент содержит логин, заданный при регистрации.<br/>- Если пользователь регистрировался через социальный Брокер, элемент содержит технический логин, сгенерированный Паспортом.

#### uid
Уникальный идентификатор (UID) учетной записи

#### uid->hosted
Признак аккаунта Почты для доменов.<br/><br/>Если флаг `hosted` равен `true` (в XML: `1`), то этот аккаунт зарегистрирован в Почте для доменов. В этом случае у элемента `uid` появляются дополнительные свойства, перечисленные ниже.

#### uid->domid
Идентификатор домена ПДД, на котором зарегистрирован аккаунт.<br/><br/>Только для аккаунтов ПДД.

#### uid->domain
Имя домена ПДД, на котором зарегистрирован аккаунт.<br/><br/>Только для аккаунтов ПДД.

#### uid->mx
Признак настройки MX записи для ПДД домена.<br/><br/>Только для аккаунтов ПДД.

#### uid->domain_ena
Признак активного домена ПДД.<br/><br/>Если домен не активен, входящие письма для этого домена принимаются, но пользователи не могут авторизоваться. Только для аккаунтов ПДД.

#### uid->catch_all
Признак адреса ПДД по-умолчанию.<br/><br/>Если флаг выставлен в `true` (в XML `1`), это означает, что переданный в запросе e-mail не найден, но у этого ПДД домена настроен ящик для доставки почты по-умолчанию и в ответе вернули именно его.

#### uid->value
В Json-ответе - значение UID пользователя
