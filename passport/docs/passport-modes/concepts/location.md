# Доступ к режимам Паспорта

Вызовы программных интерфейсов Паспорта регулируются с помощью грантов — разрешений, зафиксированных в ACL (Access Control List). Ограничения накладываются на вызов некоторых режимов, а также на использование определенных параметров.

Заявки на гранты для Паспорта следует направлять в рассылку [passport-admin@](passport-admin@yandex-team.ru). Для личных компьютеров разработчиков гранты не выдаются.


## Адреса различных Паспортов {#address}

### Тестовый Паспорт {#test}

Тестовый API Паспорта доступен по следующим URL:

- [https://passport-test.yandex.ru/passport](https://passport-test.yandex.ru/passport) — для клиентских вызовов.
- [http://passport-test-internal.yandex.ru/passport](http://passport-test-internal.yandex.ru/passport) — для серверных вызовов.

Работает с тестовой базой данных и тестовым Черным ящиком ([http://pass-test.yandex.ru/blackbox](http://pass-test.yandex.ru/blackbox)). Авторизационные куки, выписанные тестовым Паспортом, невалидны для боевого Паспорта.

### Боевой Паспорт {#production}

Боевой API Паспорта доступен по следующим URL:

- [https://passport.yandex.ru/passport](https://passport.yandex.ru/passport) — для клиентских вызовов (доступен извне Яндекса).
- [http://passport-internal.yandex.ru/passport](http://passport-internal.yandex.ru/passport) — для серверных вызовов.

Работает с боевым Черным ящиком ([http://blackbox.yandex.net/blackbox](http://blackbox.yandex.net/blackbox)). Предназначен только для вызовов с боевых серверов сервисов. Авторизационные куки, выписанные боевым Паспортом, невалидны для тестового Паспорта.

Раздел [https://doc.yandex-team.ru/blackbox/concepts/blackboxLocation.xml](https://doc.yandex-team.ru/blackbox/concepts/blackboxLocation.xml) документа [Программный интерфейс сервиса Яндекс.blackbox](https://doc.yandex-team.ru/blackbox/concepts/about.xml)