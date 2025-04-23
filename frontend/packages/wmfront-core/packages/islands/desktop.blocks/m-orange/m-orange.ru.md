## Общее

Получение и управление уведомлениями в Интранете.

**минимальный набор параметров**

```js
{
    block: 'm-orange',
    js: { parentOffset: 'island' }
}
```

**все параметры**

```js
{
    block: 'm-orange',
    js: {
        parentOffset: 'island', // обязательный
        api: 'https://path.to.backend',
        offset: 17,
        notificationsLimit: 50,
        closedQueryTime: 60000,
        openedQueryTime: 10000,
        markAsReadTime: 3000,
        repeatOnErrorTime: 3000,
        requestTimeout: 4000
    }
}
```

### API

  * `parentOffset` — **обязательный параметр**: родительский блок (`this.findBlockOutside(this.params.parentOffset)`), от нижней границы которого до конца окна будет нарисована паранджа попапа.
  * `api` — путь к ручке, **переписывает статическое свойство**, таким образом нельзя использовать 2 `m-orange` на одной странице, ходящих в разные ручки, это свойство удобно, если нужно переключиться в тестовую ручку сервиса orange при тестировании вашего сервиса.
  * `offset` — отступы попапа по краям от окна (паранджи) в пикселях.
  * `notificationsLimit` — количество загружаемых уведомлений при открытии попапа, остальные догружаются по мере скролла.
  * `closedQueryTime` — частота запросов за статусом счетчика в закрытом состоянии в миллисекундах.
  * `openedQueryTime` — частота запросов за статусом счетчика в открытом состоянии в миллисекундах.
  * `markAsReadTime` — все загруженные сообщения помечаются прочитанными через это время в миллисекундах.
  * `repeatOnErrorTime` — для некоторых запросов: если запрос вернулся с ошибкой, то повторить его через это время в миллисекундах.
  * `requestTimeout` — таймаут запросов к ручке в миллисекундах.

#### Константы

```
DEFAULT_OFFSET: 17,
DEFAULT_LIMIT: 50,
DEFAULT_CLOSED_QUERY_TIME: 60000,
DEFAULT_OPENED_QUERY_TIME: 10000,
DEFAULT_MARK_AS_READ_TIME: 3000,
DEFAULT_REPEAT_ON_ERROR_TIME: 3000,
DEFAULT_REQUEST_TIMEOUT: 4000,

API_HOST: 'https://orange.yandex-team.ru'
```
