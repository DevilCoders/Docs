# Счетчики
Инструменты для отправки счетчиков

[📹 Доклад про счетчики](https://yadi.sk/i/8z5NOwIE5QoYgQ)

## Основное
Для того чтобы посчитать [ctr](https://h.yandex-team.ru/?https://en.wikipedia.org/wiki/Click-through_rate), нужно отправить два счетчика. На показ и на клик.

## Виды счетчиков

* `blockstat` – лог, который пишется на сервере и отправляется в [mapreduce](https://h.yandex-team.ru?https://ru.wikipedia.org/wiki/MapReduce) кластер. [ℹ️ Подробнее](https://wiki.yandex-team.ru/statbox/availabledata/blockstatlog/)
* `redir` – лог, который пишется на специальном HTTP-сервере, который называется кликдемон. На него отправляется запрос с клиента [ℹ️ Подробнее](https://wiki.yandex-team.ru/statbox/availabledata/redirlog/)

У счетчиков `redir` есть несколько классов. Они задаются в поле `dtype` [ℹ️ Подробнее](https://wiki.yandex-team.ru/search-interfaces/multimedia/images/counters/islands/strediwebwhento/)

`dtype`:
* `iweb` – для действий пользователя
* `stred` – для технической информации

### Путь счетчика
У всех счетчиков есть параметр `path`. Это идентификатор счетчика.

Путь счетчика должен начинаться со страницы, с которой он отправляется.
* `search` – выдача
* `index` – морда
* `viewer` – просмотрщик

Путь счетчика должен заканчиваться на название действия.
* `click` – клик
* `show` – показ
* `open` – открытие
* `close` – закрытие

Путь счетчика показывает вложенность компонента на странице.
* `/index/snippet/button/click`

#### Кодирование пути
Для отправки счетчика, его путь должен быть закодирован [словарём blockstat](https://stat.yandex-team.ru/DictionaryEditor/BlockStat). Делать это руками не нужно, для этого в коде есть инструменты.

☝ *Следует стараться использовать существующие ключи из словаря и по минимуму добавлять туда новые.*

В корне проекта в файле [blockstat.dict.json](blockstat.dict.json) лежит копия словаря. Её можно обновить командой `fiji counters`.

Для проверки пути можно использовать npm пакет `blockstat`.

```bash
> npx blockstat /index/snippet/button/click
629.254.440.882

> npx blockstat 629.254.440.882
index/snippet/button/click
```

### Переменные счетчика
Со счетчиком можно отправить дополнительные переменные через поле `vars`. Названия переменных должны начинаться с `-`.

```js
vars: {
    '-index': 1
    '-type': 'blogger'
}
```

☝ *Переменные можно называть без `-` в начале, если это необходимо. Но такие названия переменных должны быть закодированы [словарём blockstat](https://stat.yandex-team.ru/DictionaryEditor/BlockStat)*

## Когда отправлять
Нужно слать счетчики на любые действия пользователей.

* Клик по ссылке
* Клик по кнопке
* Открытие попапа
* Закрытие попапа
* Сабмит формы

## Что отправлять
💡 Если после изучения инструкции, все ещё не очевидно какой способ выбрать, обязательно задай вопрос в чате [💬 Dev Видео](https://t.me/joinchat/AnHOJhzLUVaJJuOg4MCTgw). Разберём кейс и дополним инструкцию.

### Простой случай
Если компонент отображается на странице сразу – это простой случай.

Для показа нужно отправить `blockstat`, для действия `redir` `iweb`. У счетчиков должен быть одинаковый путь.

### Сложный случай
Если компонент показывается только при определенном условии (например в попапе) – это сложный случай.

Для показа и для действия нужно отправить `redir` `iweb` с разными путями.

Например `/index/popup/button/show` и `/index/popup/button/click`.

### Особый случай
Если компонент показывается не сразу, но перед показом проходит через сервер – это особый случай. Например особым случаем может быть пагинация.

При особом случае нужно отправить `blockstat` для показа при обработке данных на сервере и `redir` `iweb` для действия на клиенте.

## Как отправлять
### На сервере
#### В video-viewer
1. Добавить вызов в [getCounters.ts](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/video-viewer/src/components/DataProvider/DataProvider.utils/getCounters.ts)
2. Добавить новый счетчик в тайпинги [VideoViewer.typings](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/video-viewer/src/components/VideoViewer/VideoViewer.typings/index.ts)

☝ *Индекс счетчика в `getCounters` это его `name`, который нужно будет использовать на клиенте*

```js
{
    //...
    viewerButtonClick: counter.data({ // viewerButtonClick - name счетчика
        path: '/viewer/button/click',
    }),
    //...
}
```

### На клиенте
1. При разработке компонента предусмотреть callback в том месте, где нужна будет отправка счетчика
2. Обернуть компонент в [withCounters](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/video-viewer/src/lib/Counters/withCounters)

#### Счетчик на действие
```js
import { withCounters, CounterType } from '../../../lib/Counters';

export interface LinkProps {
    onClick: () => void
}

const LinkPresener: FC<LinkProps> = ({onClick, ...props}) => <a onClick={onClick} {...props}/>;

export const Link = withCounters<LinkProps>(Link, {
    events: {
        onClick: {
            name: 'viewerButtonClick', // - name счетчика c сервера
            type: CounterType.stred | CounterType.iweb // По умолчанию CounterType.iweb
            getVars: (props: LinkProps) => void; // Получает props, возвращает vars для счетчика
        }
    }
})
```

#### Счетчик на показ
```js
import { withCounters, CounterType } from '../../../lib/Counters';

export interface LinkProps {
    onShow: () => void
}

const LinkPresener: FC<LinkProps> = ({onShow, ...props}) => {
    useEffect(onShow, []);

    return <a {...props}/>;
};

export const Link = withCounters<LinkProps>({
    events: {
        onShow: { name: 'viewerLinkClick' }
    }
})(LinkPresener)
```

#### Отправка вручную
☝ *Используйте отправку вручную только если правильно отправить счетчик стандартным методом невозможно*

Если для отправки счетчика нужны очень сложные условия, или состояние из `state`, можно воспользоваться отправкой вручную.

```js
import { useCounterStred, useCounterIweb } from '../../../lib/Counters';

export interface LinkProps {
    i: number
}

export const Link: FC<LinkProps> = ({number, ...props}) => {
    const stred = useCounterStred();
    const iweb = useCounterIweb();
    const [prevNumber, setPrevNumber] = useState(number);

    useEffect(() => {
        stred('viewerLinkNumber', { '-number': prevNumber });
        iweb('viewerLinkNumber', { '-number': prevNumber });

        setPrevNumber(number);
    }, [number]);

    return <a {...props}/>;
};
```

## Как проверить что отправились
### На клиенте
Для проверки счетчиков на клиенте нужно использовать `?exp_flags=validate_counters`. Этот флаг включает логирование отправки счетчиков в консоль.

В инспекторе во вкладке `Network` можно найти запрос счетчика отфильтровав по закодированному пути *(например `path=629.254.440.882`)*

### На сервере
При запуске для разработки `templar` создаёт новый файл логов blockstat. Нужно убедиться, что счетчик записан в этот файл.

Папка, в которой создаётся файл вида в параметре `--logs` при запуске dev сервера.

Допустим логи лежат в папке `--logs /Users/username/.yandex-int/logs/rr`.

Чтобы проверить счетчик, нужно:
* Очистить папку `/Users/username/.yandex-int/logs/rr`
* Запустить dev сервер
* Открыть страницу в браузере
* Найти в папке `/Users/username/.yandex-int/logs/rr` лог с blockstat в названии файла (например `current-report-renderer_blockstat-12345`) и открыть
* Найти в файле нужную запись лога по пути счетчика *(например `/viewer/button/click`)*

## Как проверить что записались
Чтобы проверить, что счетчики пишутся, надо сделать запрос в [mapreduce](https://h.yandex-team.ru?https://ru.wikipedia.org/wiki/MapReduce).

Запрос можно выполнить в сервисе [yql.yandex-team.ru](https://yql.yandex-team.ru/) используя синтаксис [YQL](https://yql.yandex-team.ru/docs/).

### На клиенте
Логи счетчиков лежат в кластере `hahn` по пути `/logs/redir-log/`.

Пример запроса
```sql
USE hahn; /* Название кластера */

SELECT * /* Можно указать конкретные поля через , */
FROM `//logs/redir-log/30min/2020-07-17T16:00:00` /* 30min, можно указать 1h или 1d */
WHERE
    `dict`['dtype'] == 'iweb' and /* dtype счетчика */
    `dict`['path'] == '629.254.440.882' /* path счетчика */
```

[Пример результата](https://yql.yandex-team.ru/Operations/XxWveCAsJQvJeImKj200rEgizMsYSOXEJOBl63-JKBw=)

### На сервере
Логи счетчиков лежат в кластере `hahn` по пути `/logs/video-blockstat-log`.

Пример запроса
```sql
USE hahn; /* Название кластера */

SELECT * /* Можно указать конкретные поля через , */
FROM `//logs/video-blockstat-log/30min/2020-07-19T13:30:00` /* 30min, можно указать 1h или 1d */
WHERE
    blocks like '%/viewer/button/click%' /* path счетчика */
LIMIT 10 /* ограничение количества результатов, чтоб быстрее было */
```

[Пример результата](https://yql.yandex-team.ru/Operations/XxWyPWim9Yp5H_5nk7UcWmydCdXkdKI-ffMNZZwIeoo=)

## Как написать тест
### На клиенте

* Выполнить действие
* Получить `reqid`
* Вызвать [yaCheckClientCounter](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/runner/hermione/commands/yaCheckClientCounter.js), передав путь счетчика

```js
return this.browser
    .click(PO.viewer.button())
    .getReqId(PO.page()).then((reqid) => this.browser.yaCheckClientCounter(reqid, {
        path: '/viewer/button/click'
    }))
```


### На сервере
* Получить `reqid`
* Вызвать [yaCheckServerCounter](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/runner/hermione/commands/yaCheckServerCounter.js), передав путь счетчика

```js
return this.browser
    .click(PO.viewer.button())
    .getReqId(PO.page()).then((reqid) => this.browser.yaCheckServerCounter(reqid, {
        path: '/viewer/button/click'
    }))
```
