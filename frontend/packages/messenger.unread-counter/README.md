# Ручка счётчика непрочитанных сообщений

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.unread-counter/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.unread-counter)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.unread-counter)<br>
[![dep health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.unread-counter)](https://oko.yandex-team.ru/pkg/@yandex-int/messenger.unread-counter)

## Установка

```
npm i @yandex-int/messenger.unread-counter --registry=http://npm.yandex-team.ru
```

## Использование

```js
import UnreadCounter from '@yandex-chats/unread-counter';

const chatUnreadCounter = new UnreadCounter({
    url: 'https://yandex.ru/messenger/api/unread_count',
    callback: function(data) {
        console.log('Chat unread counter', data);
    }
});
```

## Описание
Пока кнопка у виджета не нажата происходит поллинг [ручки непрочитанных](https://yandex.ru/messenger/api/unread_count). После нажатия на кнопку поллинг отключается, данные передаются из IFRAME чатов с помощью postMessage.

Чтобы снизить нагрузку на ручку, в ответе сервера отдаётся поле `Ttl`.
`Ttl` — время (в секундах) через которое необходимо сделать перезапрос, обязательное поле в ответе сервера, без  него поллинг отключается.
Проверено на практике, без `Ttl` нагрузка на сервер увеличивается в 5 раз.

Если у пользователя есть история общения, то `Ttl`равен 10 сек. Если нет истории, то 60 сек.

Запросы к ручке не делаются, если:
- Ответ ручки сохранён в localStorage и ещё не устарел.
- Поменялась авторизация, наличие куки yandex_login).
- Вкладка скрыта (document.hidden).
- Первый запрос к ручке также не делается, если вкладка открыта в фоне.
- Отсутствует сеть (navigator.isOnLine).

При ошибках авторизации, таймаут перезапроса устанавливается в максимальное значение — 5 минут.
При серверных ошибках (5XX), таймаут перезапроса увеличивается в два раза относительно текущего.

## Окружение
### Production
Для Яндекс.Чатов: https://yandex.ru/messenger/api/unread_count
Для внутреннего Q: https://backend.messenger.yandex-team.ru/unread_count

### Testing (тестовый паспорт)
Для Яндекс.Чатов: https://backend.messenger.test.yandex.ru/unread_count
Для внутреннего Q: https://backend.messenger.test.yandex-team.ru/unread_count


### Development (прод. паспорт)
Для Яндекс.Чатов: https://backend.messenger.alpha.yandex.ru/unread_count
Для внутреннего Q: https://backend.messenger.alpha.yandex-team.ru/unread_count
