## Доступы при скачивании файлов

Здесь речь пойдет о страницах для скачивания файлов, то есть о страницах, унаследованных от `StreamPage`.

### Проблема

На протяжении долгого времени не было механизма проверки доступа конкретного пользователя к скачиванию файла. Таким образом, при наличии прямых ссылок на скачивание пользователь мог скачать чужой отчет/акт/договор и так далее.

### Решение

На html страницах для подобной проверки осуществляется поход в кокон, здесь будет использоваться аналогичное решение.

#### Передача параметров в репозитории ПИ

При добавлении конфигов страницы в `configs/route` нужно убедиться, что в качестве параметров урла страницы используются `platformType` и `campaignId`, а также в объект конфига передаются параметры `isPlatformPage` и `conditions`.

```typescript
const {kebabCase} = require('lodash');
const {Groups} = require('../../rights');
const {CAMPAIGN_PLATFORM} = require('../../platforms');

const routes = [
    {
        name: 'market-partner:file:dummy-page:get',
        pattern: '/api/<platformType>/<campaignId>/dummy-page',
        data: {
            method: 'GET',
            pageName: 'StreamDummyPage',
            pageData: {
                authOnly: true,
                method: 'download',
                skipCheckSecretKey: true,
            },
            group: Groups.default,
        },
        isPlatformPage: true,
        conditions: {platformType: kebabCase(CAMPAIGN_PLATFORM.DUMMY_TYPE)},
    },
];

module.exports = routes;
```

После этого нужно убедиться, что в компоненте, где размещена ссылка на скачивание файла, также передаются необходимые параметры.

```typescript
<ButtonWithoutTld
    to="market-partner:file:dummy-page:get"
    params={{campaignId, platformType: PLATFORM_TYPE.DUMMY_TYPE}}
    variant="action"
>
    <I18n id="common.common:button.download" />
</ButtonWithoutTld>
```

#### Конфиги в коконе

Далее нужно добавить имя страницы в [конфиги кокона](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets) по аналогии с новыми обычными html страницами (кабинет определяется в зависимости от platformType из предыдущего пункта).

#### Создание StreamPage

Теперь осталось создать страницу в папке `app/stout/pages/files` (например, `StreamDummyReport`). Здесь самое главное - новая страница создается не от StreamPage, как раньше, а от StreamPlatformPage.

```typescript
import StreamPlatformPage from 'app/stout/pages/abstract/platform/StreamPlatformPage';

import {promiseToResponse} from 'app/utils/promise';
import type {StoutPage} from '@yandex-market/mandrel/context';

/**
 * @constructor
 * @extends {StreamPlatformPage}
 */
function StreamDummyReport(this: StoutPage) {}

StreamDummyReport.prototype.download = function () {
    const {campaignId} = this.request.params;

    this.filename = `dummy file.pdf`;

    this.response.on('pipe', () => this.setContentDisposition());

    const result = this.attachStreamResource('dummyBackend.dummyRequest', {
        streamTo: this.response,
        campaignId,
    });

    return promiseToResponse(result);
};

module.exports = StreamPlatformPage.create(StreamDummyReport);
```

Готово!
