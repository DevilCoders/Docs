## Создание Api-страниц

Новые api-страницы наследуем от [ApplicationApiPage](pages/abstract/ApplicationApiPage.js), для преобразования ответов используем резолверы.

### Пример кода

```js
'use strict';

import _ from 'lodash';

import ApplicationApiPage from 'app/pages/abstract/ApplicationApiPage';
import {resolveVendor} from 'app/resolvers/vendor';

/**
 * Конструктор не нужен. Вызов метода и обработка результата осуществляется на уровне ApplicationApiPage
 * @constructor
 * @extends {ApplicationApiPage}
 */
const ApiFiles = ApplicationApiPage.create();
const ApiError = ApiFiles.Error;

const MAX_FILE_SIZE = 40 * 1024 * 1024;

module.exports = ApiFiles;

/**
 * Расширь прототип необходимыми методами, которые будут вызываться в рамках api.
 * Приветствуется документация и описание ручки.
 * Использовать this не нужно, все приходит в параметре, поэтому можно использовать стрелочные функции
 * Возвращает промис, поэтому можно использовать async/await.
 * @return {Promise}
 */
ApiFiles.prototype.uploadFile = async ({request, user, resource, resolverContext}) => {
    const {uid} = user;
    const {vendorId, serviceKey} = request.params;
    const vendor = await resolveVendor(resolverContext, {uid, vendorId});
    const brandId = _.get(vendor, 'brand.id');

    // так можно кинуть ошибку из страницы
    if (_.size(request.files.file.data) > MAX_FILE_SIZE) {
        throw ApiError.createError(ApiError.CODES.BAD_REQUEST, {
            statusCode: 400,
            code: 'BAD_REQUEST',
            details: {
                file: 'FILE_TOO_LARGE',
            },
        });
    }
    return resource('vendors.uploadFile', {
        uid,
        brandId,
        file: request.files.file,
        serviceKey,
    });
};
```

### Пример тестов

Тесты страниц пишем на jest в директории `app/pages/spec`

Ниже приведены наиболее частые кейсы:
- Проверка вызова резолвера
- Проверка вызова ресурса
- Проверка ответа ручки
- Проверка обработки ошибок

```js
'use strict';

import {makeJsonApiPageContext, mockParentPage} from 'app/pages/spec/helpers/mocks';
import ApiPage from 'app/pages/api/ApiPage';

// мокаем родительскую страницу, и коды ошибок для нее
jest.mock('app/pages/deprecated/ApplicationApiPage', () => mockParentPage({errorCodes: {
    BAD_REQUEST: 'mockBadRequest',
}}));

// так можно мокать резолверы
let mockResolver;
jest.mock('app/resolvers/vendors', () => (
    {
        resolveVendor: (...args) => mockResolver(...args),
    }
));

const UPLOAD_FILE_RESOURCE = 'vendors.uploadFile';

describe('ApiPage', () => {
    let resolverResult;
    let user;
    const vendorId = 123;
    const uid = 333;
    let data;
    let resolverContext;
    let apiPage;
    let params;

    beforeEach(() => {
        resolverResult = {
            vendorId,
            brand: {
                id: brandId,
            },
        };
        user = {
            uid,
        };
        mockResolver = jest.fn(() => resolverResult);
        resolverContext = {
            a: 123,
        };
        apiPage = new ApiPage();
        params = {
            vendorId,
        };
        data = new Array(5);
    });

    describe('uploadFile', () => {
        it('Вызывает резолвер', async () => {
            expect.assertions(1);
            // так готовится параметр контекст, с которым вызываются методы страниц
            const {context} = makeJsonApiPageContext({
                params,
                user,
                resolverContext,
                files,
            });

            await apiPage.uploadFile(context);

            expect(mockResolveVendor).toBeCalledWith(resolverContext, {uid, vendorId});
        });

        it('Отправляет файл в ресурс с правильными параметрами', async () => {
            expect.assertions(1);
            // контекст и метод получения моков ресурсов
            const {context, getResourceMock} = makeJsonApiPageContext({
                params,
                user,
                resolverContext,
                files,
            });

            await apiPage.uploadFile(context);

            // так можно проверить, что конкретный ресурс был вызван
            // для каждого ключа ресурса создается свой jest.fn()
            expect(getResourceMock(UPLOAD_FILE_RESOURCE)).toBeCalledWith(
                UPLOAD_FILE_RESOURCE,
                {
                    uid,
                    data,
                }
            );
        });

        it('Возвращает результат запроса ресурса', async () => {
            expect.assertions(1);
            const expectedResult = {
                success: true,
            };

            const {context} = makeJsonApiPageContext({
                params,
                user,
                resolverContext,
                files,
                // так можно мокать ответы конкретного ресурса
                resourceStubs: {
                    [UPLOAD_FILE_RESOURCE]: {
                        resolve: expectedResult,
                    },
                },
            });

            const result = await apiPage.uploadFile(context);

            expect(result).toBe(expectedResult);
        });

        it('обрабатывает ошибку', async () => {
            expect.assertions(1);
            // это должно вызвать ошибку
            files.file.data.length = (40 * 1024 * 1024) + 1;

            const {context} = makeJsonApiPageContext({
                params,
                user,
                resolverContext,
                files,
            });

            let error;

            try {
                await apiPage.uploadFile(context);
            } catch (err) {
                error = err;
            }

            expect(error).toEqual({
                // мок кода ошибки, описанный в начале
                code: 'mockBadRequest',
                error: {
                    statusCode: 400,
                    code: 'BAD_REQUEST',
                    details: {
                        file: 'FILE_TOO_LARGE',
                    },
                },
            });
        });
    });
});

```

## Создание Резолверов

Для обработки данных бэкэндов, комбинирования запросов к ручкам и преобразования данных используем резолверы, виджеты больше не используем.

### Пример кода
```js
'use strict';

/**
 * Отвечает за получение вендора.
 */

import {createResolver, unsafeResource} from '@yandex-market/mandrel/resolver';
import {responsifyPromise} from '@yandex-market/mandrel/lib/helpers';
import {flow} from 'lodash';

const resolveSomething = createResolver(
    // параметры вызова ресурсов нужно прокидывать снаружи
    // что бы не быть привязанным к контексту выполнения
    (ctx, {id, uid}) =>
        unsafeResource(ctx, 'resource.name', {uid, id})
            // одно из назначений резолверов - постобработка данных
            // обработку данных теперь делаем в резолверах
            .then(result => result.data),
    {
        cache: {
            level: 'shared',
            ttl: 30 * 60,
            key(ctx, {uid, id}) {
                return [uid, id];
            },
        },
    });

// так мы создаем резолвер, который вернет респонс
// это нужно только, если нужно использовать его в старых страницах
const resolveSomethingRequest = flow([
    resolveSomething,
    responsifyPromise,
]);

module.exports = {
    resolveVendor,
    resolveVendorRequest,
};
```

### Пример тестов

```js
'use strict';

import {resolveVendor} from 'app/resolvers/vendor';

let mockUnsafeResource;
jest.mock('@yandex-market/mandrel/resolver', () => ({
    createResolver: resolver => resolver,
    unsafeResource: (...args) => mockUnsafeResource(...args),
}));

describe('resolveVendor', () => {
    const resourceResult = {success: true};
    const resolverContext = {a: 1};
    const resolverParams = {uid: 213, vendorId: 3};
    beforeEach(() => {
        mockUnsafeResource = jest.fn(() => Promise.resolve(resourceResult));
    });

    it('Вызывает ресурс vendors.getVirtualVendorInfo с правильными параметрами', async () => {
        await resolveVendor(resolverContext, resolverParams);

        expect(mockUnsafeResource).toBeCalledWith(resolverContext, 'vendors.getVirtualVendorInfo', resolverParams);
    });

    it('Возвращает результат работы ресурса', async () => {
        const result = await resolveVendor(resolverContext, resolverParams);
        expect(result).toBe(resourceResult);
    });
});
```
