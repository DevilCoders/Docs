# Как протестировать изменения в Arcanum

В арке нет вебхуков, поэтому мы реагируем на события из Logbroker. Структурная единица, в которую вливаем ревью-реквесты - это просто папка.
При влитии ревью-реквестов из вашей папки в arc MQ вливает код в репозиторий-зеркало из GitHub. Маппинг GitHub на arc нужно сконфигурить.
Итого, для тестового стенда нам нужен чтец (далее консьюмер), репозиторий в GitHub, директория в Аркадии и маппинг в генезисе.

## Завести тестовый консьюмер

1. В аккаунте [FEI](https://lb.yandex-team.ru/lbkx/accounts/fei?page=browser&type=account) есть несколько директорий. Зайдите в папку `dev` чтобы создать тестовый консьюмер. В верхнем правом углу нажимаем на выпадающую кнопку **+ New resource → Consumer**.

<img src="https://jing.yandex-team.ru/files/zumra6a/2020-06-22T09%3A26%3A51Z.png" width="700">

2. Заполняем всплывающую форму.

<img src="https://jing.yandex-team.ru/files/zumra6a/2020-06-22T09%3A28%3A55Z.png" width="700">

* Name: __Название тестового консьюмера__
* ABC service: __ABC сервис__ (опционально)
* Responsible: __Ответственные за консьюмера__ (опционально)
* Supported codecs: __raw__
* Limits mode: __wait__

Нажимаем на **Confirm**.

3. Указываем читаемые консьюмером топики

Переходим в настройки консьюмера

<img src="https://jing.yandex-team.ru/files/zumra6a/2020-06-22T09%3A30%3A15Z.png" width="700">

На левом сайдбаре открываем вкладку Configuration.

<img src="https://jing.yandex-team.ru/files/zumra6a/2020-06-22T09%3A30%3A56Z.png" width="700">

Ниже есть кнопка для добавления правил чтения **Add read rule**, нажимаем, во всплывающей форме указываем правила чтения.

<img src="https://jing.yandex-team.ru/files/zumra6a/2020-07-16T07%3A39%3A03Z.png" width="700">

<img src="https://jing.yandex-team.ru/files/zumra6a/2020-07-16T07%3A34%3A24Z.png" width="700">

* Topic: __arcanum/prod/events/all__
* Type: __All original__

Важно!: Арканум пишет сообщения в топик __arcanum/prod/events/all__


## Аутентификация

Для чтения из Logbroker необходимо авторизовать консьюмера, для аутентификации используется oAuth-токен, который можно получить по [ссылке](http://oauth.yandex-team.ru/authorize?response_type=token&client_id=11515c5e5e994dfe8196ccfd6eb42dd8).

### Тестовый код для проверки чтения

<img alt="consumer path" src="https://jing.yandex-team.ru/files/isqua/Screenshot%202021-07-09%20at%2012.56.20.png" width="700">

* consumer - __/fei/dev/{название консьюмера}__, это должен быть полный путь, его можно скопировать в UI Logbroker.
* token - можно получить по [ссылке](http://oauth.yandex-team.ru/authorize?response_type=token&client_id=11515c5e5e994dfe8196ccfd6eb42dd8).

```js
(async () => {
    try {
        const { ArcanumConsumer } = require('@yandex-int/si.ci.arcanum-consumer');

        const consumer = new ArcanumConsumer({
            hostname: 'lbkx.logbroker.yandex.net',
            topics: ['arcanum/prod/events/all'],
            clientId: '<название консьюмера>',
            token: '<oAuth-токен>'
        });

        consumer.on('arcHeadsUpdated', console.log);
        consumer.on('error', console.error);

        await consumer.connect();
    } catch (e) {
        console.error(e);
    }
})();
```


## Настройки маппинга GitHub → Arcadia

В [генезис](https://genisys.yandex-team.ru/rules/search-interfaces.arcadia-github/default) нужно добавить секцию про тестовый репозиторий в GitHub и тестовой директории в Аркадии.

```yaml
- github:
    role: main
    owner: <овнер или организация репозитория>
    repo: <название репозитория>
    branch: <разработческая ветка репозитория>
  arcadia:
    role: mirror
    path: <путь директории в Аркадии>
  mergeQueue:
    dist: testing
```


## Запуск MQ

```console
export USE_ARCANUM=true

export MQ_DIST=testing
export MQ_DIST_FILTER_PATH=<путь директории в Аркадии>

export LOGBROKER_CLIENT_ID=<название консьюмера>
export LOGBROKER_TOKEN=<OAuth-токен>

export DEBUG=*

npm run merge-queue
```
