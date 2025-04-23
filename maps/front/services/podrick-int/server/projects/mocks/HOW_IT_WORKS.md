# Как это работает

Предположим, мы хотим протестировать в Картах карточку организации. Пишем тест, в котором открываем Я.Карты с нужной
 организацией:
```js
describe('Карточка POI.', function () {
    const url = 'https://l7test.yandex.ru/maps-prod/?ll=30.317848%2C59.927611&z=19&poi%5Bpoint%5D=30.317977%2C59.927494&poi%5Buri%5D=ymapsbm1%3A%2F%2Forg%3Foid%3D1137222840&mode=poi';

    beforeEach(function () {
        return this.browser
            .openPage(url, {mock: false});
    });
````

Когда мы запустим тест на выполнение, он сделает запрос на указанный нами урл `https://l7test.yandex.ru/maps-prod/?...`.
Запрос попадёт в nodejs-приложение Яндекс.Карт, которое сформирует свой запрос, который полетит уже от Яндекс.Карт в
 поисковый бекенд, чтобы запросить данные об организации. То есть, внутри теста мы сделали такой запрос:
```
https://l7test.yandex.ru/maps-prod/?ll=30.317848%2C59.927611&z=19&poi%5Bpoint%5D=30.317977%2C59.927494&poi%5Buri%5D=ymapsbm1%3A%2F%2Forg%3Foid%3D1137222840&mode=poi
```

А в поисковый бекенд полетел совсем другой запрос — настоящий, — гораздо более подробный:
```
http://search.maps.yandex.net/1.x/?format=json&original_host=l7test.yandex.ru&original_uri=%2Fmaps-prod%2Fapi%2Fsearch%3FcsrfToken%3D549d35c37f41811ae1ac24c3ca3f31e07735879b%253A1496835863497%26sessionId%3D1496835863436_269965%26host_config%255Bhostname%255D%3Dautotests%26lang%3Dru_RU%26yandex_gid%3D51%26origin%3Dmaps-restore%26results%3D1%26snippets%3Dmasstransit%252F1.x%252Cpanoramas%252F1.x%252Cbusinessrating%252F2.x%252Cbusinessreviews%252F1.x%252Cphotos%252F1.x%252Cexchange%252F1.x%252Cfuel%252F1.x%252Clinks%252F1.x%252Crealty%252F1.x%26type%3Dbiz%26business_oid%3D1131840699%26serpid%3D1490100690115344-372333062-man1-7821%26parent_reqid%3D1490100690115344-372333062-man1-7821&referer=http%3A%2F%2Fl7test.yandex.ru%2F&remote_ip=2a02%3A6b8%3Ac01%3A103%3A0%3A1400%3A0%3A23&user_agent=Mozilla%2F5.0%20(X11%3B%20Linux%20x86_64)%20AppleWebKit%2F537.36%20(KHTML%2C%20like%20Gecko)%20Chrome%2F53.0.2785.143%20Safari%2F537.36&yandex_fuid01=&yandex_uid=4387422041496835863&geometry=1&experimental_business_show_closed=1&experimental_distinguish_layers=1&yabs=page%3A144&type=biz&experimental_highlight_direct=1&csrfToken=549d35c37f41811ae1ac24c3ca3f31e07735879b%3A1496835863497&sessionId=1496835863436_269965&lang=ru_RU&yandex_gid=51&origin=maps-restore&results=1&snippets=masstransit%2F1.x%2Cpanoramas%2F1.x%2Cbusinessrating%2F2.x%2Cbusinessreviews%2F1.x%2Cphotos%2F1.x%2Cexchange%2F1.x%2Cfuel%2F1.x%2Clinks%2F1.x%2Crealty%2F1.x&business_oid=1131840699&serpid=1490100690115344-372333062-man1-7821&parent_reqid=1490100690115344-372333062-man1-7821
```
В ответ на этот запрос поисковый бекенд отдаёт нам
[JSON с реальными данными](http://search.maps.yandex.net/1.x/?format=json&original_host=l7test.yandex.ru&original_uri=%2Fmaps-prod%2Fapi%2Fsearch%3FcsrfToken%3D549d35c37f41811ae1ac24c3ca3f31e07735879b%253A1496835863497%26sessionId%3D1496835863436_269965%26host_config%255Bhostname%255D%3Dautotests%26lang%3Dru_RU%26yandex_gid%3D51%26origin%3Dmaps-restore%26results%3D1%26snippets%3Dmasstransit%252F1.x%252Cpanoramas%252F1.x%252Cbusinessrating%252F2.x%252Cbusinessreviews%252F1.x%252Cphotos%252F1.x%252Cexchange%252F1.x%252Cfuel%252F1.x%252Clinks%252F1.x%252Crealty%252F1.x%26type%3Dbiz%26business_oid%3D1131840699%26serpid%3D1490100690115344-372333062-man1-7821%26parent_reqid%3D1490100690115344-372333062-man1-7821&referer=http%3A%2F%2Fl7test.yandex.ru%2F&remote_ip=2a02%3A6b8%3Ac01%3A103%3A0%3A1400%3A0%3A23&user_agent=Mozilla%2F5.0%20(X11%3B%20Linux%20x86_64)%20AppleWebKit%2F537.36%20(KHTML%2C%20like%20Gecko)%20Chrome%2F53.0.2785.143%20Safari%2F537.36&yandex_fuid01=&yandex_uid=4387422041496835863&geometry=1&experimental_business_show_closed=1&experimental_distinguish_layers=1&yabs=page%3A144&type=biz&experimental_highlight_direct=1&csrfToken=549d35c37f41811ae1ac24c3ca3f31e07735879b%3A1496835863497&sessionId=1496835863436_269965&lang=ru_RU&yandex_gid=51&origin=maps-restore&results=1&snippets=masstransit%2F1.x%2Cpanoramas%2F1.x%2Cbusinessrating%2F2.x%2Cbusinessreviews%2F1.x%2Cphotos%2F1.x%2Cexchange%2F1.x%2Cfuel%2F1.x%2Clinks%2F1.x%2Crealty%2F1.x&business_oid=1131840699&serpid=1490100690115344-372333062-man1-7821&parent_reqid=1490100690115344-372333062-man1-7821)
об организации, которые и возвращаются в Яндекс.Карты. На основе этого JSON приложение Карт строит интерфейс панели
организации. А наше Hermione-приложение с функциональными тестами уже проверяет, что в интерфейсе Карт панель
организации отрендерилась успешно, что в ней появились DOM-узлы с нужными CSS-селекторами.

_Всё логично, однако тесты на реальных данных писать не стоит._

## Проблема
Когда в тестах мы делаем запросы в реальные бекенды, оттуда могут приходить в разное время разные ответы и _каждый раз
они будут правильными, но могут отличаться_. Например, у организации может измениться рейтинг или номер
телефона или появиться новые отзывы. Если мы будем писать тесты, получая каждый раз из поискового бекенда реальные
данные, тесты будут регулярно падать. Поэтому мы пишем тесты на моках.

## Мок
Это JSON с реальными данными, полученными из реального бекенда в некий момент времени. Что нужно сделать, чтобы
тестировать Карты на замоканных данных? Возвращаемся к нашему тесту и немного видоизменяем:
```js
describe('Карточка POI.', function () {
    const url = 'https://l7test.yandex.ru/maps-prod/?ll=30.317848%2C59.927611&z=19&poi%5Bpoint%5D=30.317977%2C59.927494&poi%5Buri%5D=ymapsbm1%3A%2F%2Forg%3Foid%3D1137222840&mode=poi';

    beforeEach(function () {
        return this.browser
            .openPage(url);
    });
````
Сам тест не изменился. Только из вызова метода `openPage` мы убрали аргумент `{mock: false}` (по умолчанию это свойство
принимает значение `true`). Что это нам дало?

Поменялись пути запросов `Тест ---> Яндекс Карты` и `Яндекс Карты ---> Поисковый Бекенд`. Незначительно.

**`Тест ---> Яндекс Карты`:**
_Появился дополнительный GET-параметр `&host_config[hostname]=autotests`_

```bash
# Было
https://l7test.yandex.ru/maps-prod/?ll=30.317848%2C59.927611&z=19&poi%5Bpoint%5D=30.317977%2C59.927494&poi%5Buri%5D=ymapsbm1%3A%2F%2Forg%3Foid%3D1137222840&mode=poi

# Стало
https://l7test.yandex.ru/maps-prod/?ll=30.317848%2C59.927611&z=19&poi%5Bpoint%5D=30.317977%2C59.927494&poi%5Buri%5D=ymapsbm1%3A%2F%2Forg%3Foid%3D1137222840&mode=poi&host_config%5Bhostname%5D%3Dautotests
```
**`Яндекс Карты ---> Поисковый Бекенд`:**
_Изменился хост поискового бекенда — заменился на хост Подрика._

```bash
# Было
                    http://search.maps.yandex.net/1.x/?format=json&original_host=l7test.yandex.ru&original_uri=%2Fmaps-prod%2Fapi%2Fsearch%3FcsrfToken%3D549d35c37f41811ae1ac24c3ca3f31e07735879b%253A1496835863497%26sessionId%3D1496835863436_269965%26host_config%255Bhostname%255D%3Dautotests%26lang%3Dru_RU%26yandex_gid%3D51%26origin%3Dmaps-restore%26results%3D1%26snippets%3Dmasstransit%252F1.x%252Cpanoramas%252F1.x%252Cbusinessrating%252F2.x%252Cbusinessreviews%252F1.x%252Cphotos%252F1.x%252Cexchange%252F1.x%252Cfuel%252F1.x%252Clinks%252F1.x%252Crealty%252F1.x%26type%3Dbiz%26business_oid%3D1131840699%26serpid%3D1490100690115344-372333062-man1-7821%26parent_reqid%3D1490100690115344-372333062-man1-7821&referer=http%3A%2F%2Fl7test.yandex.ru%2F&remote_ip=2a02%3A6b8%3Ac01%3A103%3A0%3A1400%3A0%3A23&user_agent=Mozilla%2F5.0%20(X11%3B%20Linux%20x86_64)%20AppleWebKit%2F537.36%20(KHTML%2C%20like%20Gecko)%20Chrome%2F53.0.2785.143%20Safari%2F537.36&yandex_fuid01=&yandex_uid=4387422041496835863&geometry=1&experimental_business_show_closed=1&experimental_distinguish_layers=1&yabs=page%3A144&type=biz&experimental_highlight_direct=1&csrfToken=549d35c37f41811ae1ac24c3ca3f31e07735879b%3A1496835863497&sessionId=1496835863436_269965&lang=ru_RU&yandex_gid=51&origin=maps-restore&results=1&snippets=masstransit%2F1.x%2Cpanoramas%2F1.x%2Cbusinessrating%2F2.x%2Cbusinessreviews%2F1.x%2Cphotos%2F1.x%2Cexchange%2F1.x%2Cfuel%2F1.x%2Clinks%2F1.x%2Crealty%2F1.x&business_oid=1131840699&serpid=1490100690115344-372333062-man1-7821&parent_reqid=1490100690115344-372333062-man1-7821
# Стало
http://podrick.c.maps.yandex-team.ru/mocks/search/1.x/?format=json&original_host=l7test.yandex.ru&original_uri=%2Fmaps-prod%2Fapi%2Fsearch%3FcsrfToken%3D549d35c37f41811ae1ac24c3ca3f31e07735879b%253A1496835863497%26sessionId%3D1496835863436_269965%26host_config%255Bhostname%255D%3Dautotests%26lang%3Dru_RU%26yandex_gid%3D51%26origin%3Dmaps-restore%26results%3D1%26snippets%3Dmasstransit%252F1.x%252Cpanoramas%252F1.x%252Cbusinessrating%252F2.x%252Cbusinessreviews%252F1.x%252Cphotos%252F1.x%252Cexchange%252F1.x%252Cfuel%252F1.x%252Clinks%252F1.x%252Crealty%252F1.x%26type%3Dbiz%26business_oid%3D1131840699%26serpid%3D1490100690115344-372333062-man1-7821%26parent_reqid%3D1490100690115344-372333062-man1-7821&referer=http%3A%2F%2Fl7test.yandex.ru%2F&remote_ip=2a02%3A6b8%3Ac01%3A103%3A0%3A1400%3A0%3A23&user_agent=Mozilla%2F5.0%20(X11%3B%20Linux%20x86_64)%20AppleWebKit%2F537.36%20(KHTML%2C%20like%20Gecko)%20Chrome%2F53.0.2785.143%20Safari%2F537.36&yandex_fuid01=&yandex_uid=4387422041496835863&geometry=1&experimental_business_show_closed=1&experimental_distinguish_layers=1&yabs=page%3A144&type=biz&experimental_highlight_direct=1&csrfToken=549d35c37f41811ae1ac24c3ca3f31e07735879b%3A1496835863497&sessionId=1496835863436_269965&lang=ru_RU&yandex_gid=51&origin=maps-restore&results=1&snippets=masstransit%2F1.x%2Cpanoramas%2F1.x%2Cbusinessrating%2F2.x%2Cbusinessreviews%2F1.x%2Cphotos%2F1.x%2Cexchange%2F1.x%2Cfuel%2F1.x%2Clinks%2F1.x%2Crealty%2F1.x&business_oid=1131840699&serpid=1490100690115344-372333062-man1-7821&parent_reqid=1490100690115344-372333062-man1-7821
```

- Когда в метод `browser.openPage()` передаётся параметр `{mock: true}`, в запросе к Яндекс.Картам улетает
дополнительный GET-параметр `&host_config[hostname]=autotests`.
- Карты получают этот запрос и как обычно формируют запрос к поисковому бекенду. Но благодаря параметру
`&host_config[hostname]=autotests` понимают, что запрос нужно направить не в реальный бекенд, а в Подрик.
- Поэтому второй запрос уходит уже в Подрик в ручку `/mocks/search/1.x/`.
- А Подрик умеет отдавать замоканные JSON-данные вместо реальных.


Мок — это JSON с production-данными, полученными из реального бекенда в некий момент времени. Мы этот
JSON сохранили в некоем хранилище, и теперь Подрик умеет его отдавать, если он соответствует запросу.

### Как значение `autotests` связано с Подриком?
Для того, чтобы разные карточные проекты могли дергать ручки других сервисов, урлы этих сервисов вынесены в общие
конфигурационные файлы. Например: [production хосты](https://github.yandex-team.ru/maps/hosts/blob/master/hosts/1.3/hosts-production.json),
[testing хосты](https://github.yandex-team.ru/maps/hosts/blob/master/hosts/1.3/hosts-testing.json).

Когда мы что-то ищем на Я.Картах, поисковый запрос перенаправляется в реальный Поиск, урл которого Карты получают из
[production-конфига](https://github.yandex-team.ru/maps/hosts/blob/master/inthosts/1.1/hosts-production.json#L51) —
поисковый запрос уходит в сервис http://search.maps.yandex.net/


Подобный конфиг есть и для тестирования: https://github.yandex-team.ru/maps/hosts/blob/master/inthosts/1.1/production/autotests.json
```json
{
    "searchApi": "http://podrick.c.maps.yandex-team.ru/mocks/search/",
    "weatherApi": "http://podrick.c.maps.yandex-team.ru/mocks/weather/",
    "sendmail": "http://podrick.c.maps.yandex-team.ru/mocks/sendmail/"
}
```

Если в урл запроса к Картам мы допишем GET-параметр `host_config[hostname]=autotests`, поисковый запрос
перенаправится в Подрик, урл которого Карты получат из
[autotests-конфига](https://github.yandex-team.ru/maps/hosts/blob/master/inthosts/1.1/production/autotests.json#L2) —
 вот почему поисковый запрос уйдёт в Подрик по адресу http://podrick.c.maps.yandex-team.ru/mocks/search/

### Роль Подрика в тестировании
Итак, запрос от Карт пришёл в Подрик. Что дальше?

Запрос в Подрике обрабатывается последовательно с помощью
[search-middleware](https://github.yandex-team.ru/maps/podrick/blob/master/server/projects/mocks/search/index.js) и
[mock-middleware](https://github.yandex-team.ru/maps/podrick/blob/master/server/projects/mocks/mock-middleware.js),
которые парсят запрос, из него понимают, как называется мок c замоканными реальными данными об организации, делают
запрос в Хранилище моков (мы используем S3), получают оттуда содержимое мока и отдают его назад в
Яндекс.Карты. Вся цепочка запросов и ответов выглядит так:
```
Тест --[http-request]--> Карты --[http-request]--> Подрик --[http-request]--> S3
                                                                               |
                       Карты UI <--[json-ответ]--- Подрик <---[json-ответ]-----|
```

Подрик в этой цепочке выступает в роли поискового бекенда. Его задача понять, какой мок нужно вернуть в Карты,
и сходить за этим моком в S3.

## Как создать мок-файл для определенного запроса

1. Открываем в IDE проект с тестами.
2. Cоздаём тест, где формируем урл к Картам.
3. В метод `openPage` передаём параметр `{mock: true}`. Можно и не передавать, по умолчанию он `true`.
    ```js
    describe('Карточка POI.', function () {
        const url = 'https://l7test.yandex.ru/maps-prod/?ll=30.317848%2C59.927611&z=19&poi%5Bpoint%5D=30.317977%2C59.927494&poi%5Buri%5D=ymapsbm1%3A%2F%2Forg%3Foid%3D1137222840&mode=poi';

        beforeEach(function () {
            return this.browser
                .openPage(url, {mock: true});
        });
    ````
4. Всё.

    _Когда  мы запустим тест, Карты сделают запрос в Подрик, тот поищет в S3 соответствующий запросу мок и не
    найдёт, сходит в реальный Бекенд, получит оттуда реальные данные, сохранит их в S3, а потом вернёт в Карты.
    Карты отрисуют свой интерфейс, а Hermione-тест его проверит._


:warning: **При добавлении новых моков, не забудьте внести новые хосты в соответствующий [пресет для автотестов](https://github.yandex-team.ru/maps/hosts/blob/master/CONTRIBUTING.md).** Файлы для изменения: [hosts](https://github.yandex-team.ru/maps/hosts/blob/master/hosts/1.3/production/autotests.json) и [inthosts](https://github.yandex-team.ru/maps/hosts/blob/master/inthosts/1.1/production/autotests.json).
