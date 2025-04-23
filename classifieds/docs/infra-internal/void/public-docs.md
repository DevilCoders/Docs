## Тестирование ссылок на документацию

При измененении публичной документации запустится тестирование ссылок на документации при помощи teamcity джобы [Links Test](https://t.vertis.yandex-team.ru/buildConfiguration/VertisAdmin_YandexVertisShiva_LinksTest?mode=builds).

### Возможные ошибки:

- Not 200 status code, означает что данной страницы не существует, но она используется в shiva
- Anchor not found, означает что на странице документации отсутствует якорь, то есть определенный заголовок

### Как починить?

- Заменить сломаные ссылки в [файле](https://a.yandex-team.ru/svn/trunk/arcadia/classifieds/infra/shiva/pkg/links/links.go)
- Перезапустить проверку

### Как добавить новую ссылку?

- Добавить ссылку в [файл](https://a.yandex-team.ru/svn/trunk/arcadia/classifieds/infra/shiva/pkg/links/links.go)
- Добавить переменную в [список](https://a.yandex-team.ru/svn/trunk/arcadia/classifieds/infra/shiva/pkg/links/links_test.go?rev=r9708375#L58)
