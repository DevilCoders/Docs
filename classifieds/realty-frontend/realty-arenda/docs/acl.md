# Ролевая система

## Базовый флоу разработки
Добавили/изменили/удалили новые страницы/гейты в админке, изменили статусы квартиры/поисковые пресеты - генерируем карты прав

```bash
make generate-acl-maps
```

Далее, согласно тикету, распределяем новые права в [роли](https://github.com/YandexClassifieds/realty-frontend/tree/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/acl/roles)

В деве и тестинге возможно залипнуть в роль по GET параметру (проставится кука)
```
https://arenda.test.vertis.yandex.ru/management/manager/flats/?_role=ADMIN_ROLE
```

Следить за наличием прав и ролей можно по специальной страничке
```
https://arenda.test.vertis.yandex.ru/management/my-acl/
```

## Как оперировать правами в клиентском коде?

Роль в стор прокидывается с ноды в редьюсер [user](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/view/ts-types/user.ts#L69).
Информация о заблокированном доступе в [accessDenied](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/view/modules/accessDenied/reducers.ts).
Для работы с правами для удобства сделан [контекст и хок](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/view/enhancers/withAcl.tsx#L10-L35).
Контекс пробрасывает роль, в которой доступны методы для проверки прав (о роли и методах описано ниже в доке).  
Пример использования:

```tsx
import { MapStateToProps, connect, MapDispatchToProps } from 'react-redux';
import flowRight from 'lodash/flowRight';

import { IUniversalStore } from 'view/modules/types';
import { withAclContext } from 'view/enhancers/withAcl';

import { INavbarMenuOwnProps, INavbarMenuStateProps, INavbarMenuDispatchProps } from './types';

import { NavbarMenu } from './index';

interface IRequiredStore extends Pick<IUniversalStore, 'user'> {}

const mapStateToProps: MapStateToProps<INavbarMenuStateProps, INavbarMenuOwnProps, IRequiredStore> = (state, props) => {
    const { aclRole } = props;

    const isManager = aclRole.hasPermissionByGroupConstructorParams('pages', {
              page: 'manager-search-flats',
          });

    const isPhotographer = aclRole.hasPermissionByGroupConstructorParams('pages', {
              page: 'outstaff-photographer-search-flats',
          });

    const isCallCenter = aclRole.hasPermissionByGroupConstructorParams('pages', {
              page: 'outstaff-call-center-form',
          });

    const isCopywriter = aclRole.hasPermissionByGroupConstructorParams('pages', {
              page: 'outstaff-copywriter-search-flats',
          });

    const isRetoucher = aclRole.hasPermissionByGroupConstructorParams('pages', {
              page: 'outstaff-retoucher-search-flats',
          });

    return {
        isManager,
        isCallCenter,
        isPhotographer,
        isCopywriter,
        isRetoucher,
    };
};

const mapDispatchToProps: MapDispatchToProps<INavbarMenuDispatchProps, INavbarMenuOwnProps> = {
    openMenu,
    closeMenu,
};

const NavbarMenuContainer = flowRight(
    withAclContext,
)(NavbarMenu);

export { NavbarMenuContainer };
```

Также для удобства были введены компоненты условного рендеринга [раз](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/view/components/AclRenderWithAccessToPage/index.tsx) [два](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/view/components/AclRenderWithAccessToGate/index.tsx#L10-L25)  
Пример использования:

```tsx
...
render() {
    return (
        <AclRenderWithAccessToPage page="manager-flat-form">
            <h1>Render if has access to manager-flat-form page</h1>
        </AclRenderWithAccessToPage>
    )
}
...
```

## Реализованные механизмы
1) [Точечный доступ к определенным статусам квартир](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/acl/permissions/flat-status.ts)
2) [Точечный доступ к определенным пресетам](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/acl/permissions/flat-presets.ts)
3) [Точечный доступ к определенным гейтам](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/acl/permissions/gates.ts)
4) [Точечный доступ к определенным страницам](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/acl/permissions/pages.ts)
5) [Подрезка чувствительных данным](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/acl/permissions/sensetiveData.ts)

Каждый механизм - это класс, определяющий 2 метода getData - параметры для генерации карт и generateId - функция для генерации уникального id права в картах, чтобы не было возможности пересечения прав из разных групп.

```tsx
import { AclPermission, generateAclPermissionId } from 'realty-core/app/lib/acl/acl-permission';

import { PageName } from 'view/libs/link';

interface IAclConstructorParams {
    page: PageName;
}

export const pagePermission = new AclPermission({
    getData: (params: IAclConstructorParams) => ({ ...params }),
    generateId: (params: IAclConstructorParams) => generateAclPermissionId(params.page, 'PAGE'),
});
```

Нет кейсов использовать право напрямую в бизнесовом коде, они используются в абстракциях более высокого уровня. Исключение - генерация карт автоматикой
```js
const mapPermission = pagePermission.get({ page: 'manager-flat-publishing' });

/**
   { 
      "MANAGER_FLAT_PUBLISHING_PAGE": {
            "id": "MANAGER_FLAT_PUBLISHING_PAGE",
            "page": "manager-flat-publishing"
        }
    }
 */
```

Механизмы с набором возможных вариантов значений после генерации образуют [карты прав](https://github.com/YandexClassifieds/realty-frontend/tree/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/acl/maps)

Пример:
```json
{
    "USER_PERSON_SENSITIVE_DATA": {
        "id": "USER_PERSON_SENSITIVE_DATA",
        "data": "USER_PERSON"
    },
    "USER_CONTACT_SENSITIVE_DATA": {
        "id": "USER_CONTACT_SENSITIVE_DATA",
        "data": "USER_CONTACT"
    },
    "USER_PASSPORT_SENSITIVE_DATA": {
        "id": "USER_PASSPORT_SENSITIVE_DATA",
        "data": "USER_PASSPORT"
    },
    "USER_PAYMENT_DATA_SENSITIVE_DATA": {
        "id": "USER_PAYMENT_DATA_SENSITIVE_DATA",
        "data": "USER_PAYMENT_DATA"
    },
    "FLAT_CONTRACT_SENSITIVE_DATA": {
        "id": "FLAT_CONTRACT_SENSITIVE_DATA",
        "data": "FLAT_CONTRACT"
    }
}
```

Карты должны [генерироваться на основе структуры проекта/типов/переменных](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/tools/generate-permissions.ts) используемых в коде.
Ни в коем случае нельзя руками вносить в них правки, основная мотивация - поддержка, прав генерируется много, уследить за всем руками сложно, в голове держать тоже сложно.
Чтобы сгенерировать карты запускаем команду

```bash
make generate-acl-maps
```

## Группы механизмов

Абстракция выше - над механизмами - группы механизмов, они объединяют конструктор механизма и сгенерированные карты, тоже не используются в бизнесовом коде, а только в абстракциях выше.

```tsx
export const arendaPermissionsGroup = new AclPermissionsGroup([
    {
        groupId: 'flatStatus',
        permission: flatStatusPermission,
        map: flatStatusPermissionsMap,
    } as const,
    {
        groupId: 'flatPreset',
        permission: flatPresetsPermission,
        map: flatPrestsPermissionsMap,
    } as const,
    ...
])
```

## Конструктор ролей

Абстракция выше - конструктор ролей, по названию понятно зачем она нужна.
Роли [определенные бизнес процессами](https://github.com/YandexClassifieds/realty-frontend/tree/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/acl/roles) с различным набором прав.
Внутри каждой роли перечисляются права для каждого механизма по группам.

## Роль

Роль - это абстракция обладающая рядом методов проверки прав, именно ею нужно оперировать в бизнесовом коде.

```tsx
const arendaFactoryRole = new AclRoleFactory(ArendaAclRoleType, arendaPermissionsGroup);

const { roles, permissionsGroup } = arendaFactoryRole;

export const role = arendaFactoryRole.create(roles.RETOUCHER_ROLE, {
    pages: [
        permissionsGroup.permissions.pages.OUTSTAFF_FLAT_RETOUCHER_QUESTIONNAIRE_FORM_PAGE,
        permissionsGroup.permissions.pages.OUTSTAFF_RETOUCHER_SEARCH_FLATS_PAGE,
    ],
    gates: [permissionsGroup.permissions.gates.OUTSTAFF_UPDATE_FLAT_QUESTIONNAIRE_RETOUCHER_GATE],
    flatPreset: [
        permissionsGroup.permissions.flatPreset.FLAT_NEED_RETOUCHED_PHOTO_LINK_PRESET,
        permissionsGroup.permissions.flatPreset.FLAT_NEED_COPYWRITER_REVIEW_PRESET,
    ],
    flatStatus: [
        permissionsGroup.permissions.flatStatus.FLAT_WORK_IN_PROGRESS_STATUS,
        permissionsGroup.permissions.flatStatus.FLAT_LOOKING_FOR_TENANT_STATUS,
    ],
    sensitiveData: [],
});

// имплементированы различные методы по проверке прав, например 
role.hasPermissionByGroupConstructorParams('sensitiveData', { data: SensitiveData.USER_CONTACT });

```

## Набор ролей

Но так как ролей много, для удобного оперирования ими была введена самая высокая абстракция - набор ролей, которая по id роли получает инстанс.
В основном используется, чтобы получить конструктор роли текущего пользователя.

```tsx
const arendaRoles = new AclRoles(ArendaAclRoleType, [
    accountManager,
    admin,
    callCenterOperator,
    conciergeManager,
    conciergeManagerExtended,
    coordinator,
    copywriter,
    fieldManager,
    onlineManager,
    photographer,
    retoucher,
    salesManager,
    userRole,
]);

arendaRoles.get(ArendaAclRoleType.COPYWRITER_ROLE);

// когда ролей много, можно получить "смерженную по правам роль"
arendaRoles.getWithMerge([ ArendaAclRoleType.COPYWRITER_ROLE, ArendaAclRoleType.PHOTOGRAPHER_ROLE ]);
```

Почему так сложно и много абстракций? Механизм в целом получился переиспользуемый + сильно протипизированный, правки в типах механизмов, групп механизмов, картах прав, ролях сразу же отражаются ошибками в TS.

## Подробнее о реализации механизмов

Для механизмов, которые как либо оперируют с данными из бекенда (статус квартиры, пресеты, подрезка данных, и т.п) был создан [AclResource](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-core/app/resource/realty3/acl-resource.js).
В нем переопределен pipeline хождения в бекенд, добавлены методы (specific на схеме ниже)

```
prepareRequestOpts -> aclRequest (specific) -> makeRequest -> aclResponse (specific) -> aclOmit (specific) -> process -> error
```

`aclRequest` - работа с GET параметрами, Body запроса. Например, проверяем, что в параметрах запроса только разрешенные пользователю пресеты
`aclResponse` - работа с ответом от бекенда, проверки. Например, что запрошенная по flatId квартира находится в статусе, который доступен пользователю
`aclOmit` - подрезка данных, согласно картам ПРАВО <-> Данные. [Примеры карт](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-core/app/resource/realty3/rent-moderation/acl-omit-maps.ts#L11)

Пояснение - данная карта вырежет из ответа поля ownerPerson tenantPerson во всех пришедших с бекенда договоров внутри платежей, если будет отсутствовать право `USER_PERSON_SENSITIVE_DATA`
```ts
export const userPaymentsAclOmitMap: PermissionsMap = {
    [permissionsGroup.permissions.sensitiveData.USER_PERSON_SENSITIVE_DATA]: [
        '$.response.payments[*].contract.ownerPerson',
        '$.response.payments[*].contract.tenantPerson',
    ],
};
```

Ошибку в ресурсах необходимо [выбрасывать конкретную](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-core/app/resource/realty3/acl-resource.js#L83-L89), так как только она корректно обработается и пробросится выше в приложение.

Пример:
```js
// aclResource
AclRentModerationResource
    .method('get_flats', {
        prepare(opts) {},
        aclResponse({ response }) {
            const { aclRole } = this.cfg.req;
    
            response.flats.forEach(({ flat }) => {
                const requiredPermission = aclRole
                    .getPermissionIfAccessDeniedByGroupConstructorParams('flatStatus', { status: flat.status });
    
                if (requiredPermission) {
                    this.throwAclResourceAccessDeniedError(requiredPermission.id, aclRole.getRole());
                }
            });
        }
    })
```

Перехват ошибки в приложении происходит в [базовом конструкторе страниц](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/controller/pages/page.js#L187-L197)

Для механизма подрезки прав в aclResource [предусмотрен callback](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-core/app/resource/realty3/acl-resource.js#L91-L95), который будет вызван, в случае отсутствия необходимых прав
```tsx
AclRentModerationResource
    .setAclOmitCallback(function(permission) {
        const { aclRole } = this.cfg.req;

        return Boolean(aclRole.getPermissionIfAccessDeniedByGroupAndPermissionName('sensitiveData', permission));
    })
```

Его сигнатура следующая - он работает от требуемого права, возращает Boolean, если вернет false, то произойдет выброс ошибки.

В основе механизма точечного доступа к страницам лежат исходники с роутами [раз](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/router/common/routes/manager.ts) [два](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/router/common/routes/outstaff.ts).
Отсюда есть ограничение, нельзя параметризированные по ролям роуты. Например `/management/<role>/flats/` надо разбить на `/management/manager/flats/`
В основе механизма точечного доступа к гейтам лежит файловая структура гейтов [раз](https://github.com/YandexClassifieds/realty-frontend/tree/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/controller/gates/manager) [два](https://github.com/YandexClassifieds/realty-frontend/tree/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/controller/gates/outstaff).

Централизованное место для блокирования доступа к админке [мидлвара acl](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/middlewares/admin/acl.ts).
Ошибки AclError пробрасываются на фронт в [гейтах](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-core/app/lib/middleware/gates.js#L18-L26) [страницах](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/controller/pages/page.js#L187-L197) [спа ответах](https://github.com/YandexClassifieds/realty-frontend/blob/ab033fd5cc96fe2870ad28c5bd4bb6107bd19b30/realty-arenda/app/middlewares/spa-response.js#L20-L26)


