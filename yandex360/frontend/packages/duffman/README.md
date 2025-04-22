[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/packages/duffman&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/duffman)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/packages/duffman&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/duffman)

# Duffman. Серверный фреймворк для персональных сервисов.

[Changelog](CHANGELOG.md)

[Документация Duffman](./docs/)


### Документация API

 * [ava](https://beta.wiki.yandex-team.ru/antonxolodkov/ava) - аватарница
 * [abook](https://beta.wiki.yandex-team.ru/pochta/abook/api/mail) - контакты
 * [blackbox](https://doc.yandex-team.ru/blackbox/reference/MethodUserInfo.xml) - авторизация и информация из паспорта
 * [captcha](https://doc.yandex-team.ru/Passport/captcha/concepts/api.xml) - капча
 * [furita](https://wiki.yandex-team.ru/mail/furita) - фильтры
 * [journal](https://wiki.yandex-team.ru/passport/historydb/api) - журнал
 * [mbody](https://wiki.yandex-team.ru/users/dskut/message-body)
 * [mops](https://wiki.yandex-team.ru/users/shelkovin/asyncoperations/http-interface)
 * [mpfs](https://beta.wiki.yandex-team.ru/disk/mpfs/) - бекенд Диска
 * [passport](https://beta.wiki.yandex-team.ru/passport/api) - паспорт
 * [rpop](https://beta.wiki.yandex-team.ru/users/becks/rpop/) - сборщики
 * [saas](https://beta.wiki.yandex-team.ru/jandekspoisk/saas)
 * [settings](https://wiki.yandex-team.ru/users/prez/yserversettings/)
 * [staff](https://beta.wiki.yandex-team.ru/staff/api) - стафф
 * [todo](https://wiki.yandex-team.ru/calendar/api/ext/backend/todos/) - тудушка
 * [translate](https://tech.yandex.ru/translate/doc/dg/concepts/About-docpage/) - переводчик
 * [wmi](https://wiki.yandex-team.ru/users/jkennedy/ywmiapi)
 * [smslink](https://beta.wiki.yandex-team.ru/YandexMobile/applinksms) - sms со ссылкой на приложение

---
### Требования
 - node.js >= 8.12
 - прочитать документацию до конца


### Отладка

Даффман можно запустить с `INSPECT=true` или `INSPECT=<port>` для отладки в dev-tools.
VS Code автоматически пробрасывает порт на локальную машину, можно сразу пользоваться инспектором.
Либо прокинуть порт вручную через `ssh -L <port>:127.0.0.1:<port> <host>`.
