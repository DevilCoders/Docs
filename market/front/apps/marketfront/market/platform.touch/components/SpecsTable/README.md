## Таблица с характеристиками модели или оффера

```jsx
const filters = [
    {
        id: '7893318',
        type: 'enum',
        name: 'Производитель',
        xslname: 'vendor',
        subType: '',
        kind: 1,
        position: 1,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: 'Apple',
                vendor: {
                    name: 'Apple',
                    entity: 'vendor',
                    id: 153043,
                },
                id: '153043',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '153043',
                ],
            },
        ],
    },
    {
        id: '13887626',
        type: 'enum',
        name: 'Цвет',
        xslname: 'color_glob',
        subType: 'color',
        kind: 2,
        position: 2,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                group: 'серебристый',
                found: 1,
                value: 'серебристый',
                code: '#c0c0c0',
                id: '13898623',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '13898623',
                ],
            },
        ],
    },
    {
        id: '4940921',
        type: 'enum',
        name: 'Тип',
        xslname: 'Type',
        subType: '',
        kind: 1,
        position: 3,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: 'смартфон',
                id: '13475069',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '13475069',
                ],
            },
        ],
    },
    {
        id: '12782797',
        type: 'enum',
        name: 'Линейка',
        xslname: 'vendor_line',
        subType: '',
        kind: 1,
        position: 4,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: 'iPhone X',
                vendor: {
                    name: 'Apple',
                    entity: 'vendor',
                    id: 153043,
                },
                id: '15585327',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '15585327',
                ],
            },
        ],
    },
    {
        id: '13476053',
        type: 'boolean',
        name: 'Android',
        xslname: 'androidOS',
        subType: '',
        kind: 1,
        position: 5,
        noffers: 1,
        values: [
            {
                initialFound: 0,
                found: 0,
                value: '1',
                id: '1',
            },
            {
                initialFound: 1,
                found: 1,
                value: '0',
                id: '0',
            },
        ],
    },
    {
        id: '13476171',
        type: 'boolean',
        name: 'iOS',
        xslname: 'iOS',
        subType: '',
        kind: 1,
        position: 6,
        noffers: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: '1',
                id: '1',
            },
            {
                initialFound: 0,
                found: 0,
                value: '0',
                id: '0',
            },
        ],
    },
    {
        id: '15156912',
        type: 'enum',
        name: 'Диагональ экрана',
        xslname: 'DisplayDiagonal_ENUM',
        subType: '',
        kind: 1,
        position: 7,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: '5.5"-5.9"',
                id: '15934123',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '15934123',
                ],
            },
        ],
    },
    {
        id: '12565550',
        type: 'enum',
        name: 'Разрешение экрана',
        xslname: 'ScreenRes',
        subType: '',
        kind: 1,
        position: 8,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: '2436×1125',
                id: '15084619',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '15084619',
                ],
            },
        ],
    },
    {
        id: '7808633',
        type: 'boolean',
        name: '4G LTE',
        xslname: 'LTE',
        subType: '',
        kind: 1,
        position: 9,
        noffers: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: '1',
                id: '1',
            },
            {
                initialFound: 0,
                found: 0,
                value: '0',
                id: '0',
            },
        ],
    },
    {
        id: '13443198',
        type: 'boolean',
        name: '2 SIM-карты',
        xslname: 'twosim',
        subType: '',
        kind: 1,
        position: 10,
        noffers: 1,
        values: [
            {
                initialFound: 0,
                found: 0,
                value: '1',
                id: '1',
            },
            {
                initialFound: 1,
                found: 1,
                value: '0',
                id: '0',
            },
        ],
    },
    {
        id: '15161366',
        type: 'enum',
        name: 'Память',
        xslname: 'MemoryVolumeGB_ENUM',
        subType: '',
        kind: 1,
        position: 11,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: '64 Гб',
                id: '15161367',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '15161367',
                ],
            },
        ],
    },
    {
        id: '4925675',
        type: 'boolean',
        name: 'Слот для карты памяти',
        xslname: 'FlashCardSlot',
        subType: '',
        kind: 1,
        position: 12,
        noffers: 1,
        values: [
            {
                initialFound: 0,
                found: 0,
                value: '1',
                id: '1',
            },
            {
                initialFound: 1,
                found: 1,
                value: '0',
                id: '0',
            },
        ],
    },
    {
        id: '7013269',
        type: 'boolean',
        name: 'NFC',
        xslname: 'NFC',
        subType: '',
        kind: 1,
        position: 15,
        noffers: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: '1',
                id: '1',
            },
            {
                initialFound: 0,
                found: 0,
                value: '0',
                id: '0',
            },
        ],
    },
    {
        id: '16230465',
        type: 'enum',
        name: 'Количество основных камер',
        xslname: 'RearCamNum',
        subType: '',
        kind: 1,
        position: 16,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: '2',
                id: '16230472',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '16230472',
                ],
            },
        ],
    },
    {
        id: '12616441',
        type: 'enum',
        name: 'Год анонсирования',
        xslname: 'YearOfProduction',
        subType: '',
        kind: 1,
        position: 17,
        noffers: 1,
        valuesCount: 1,
        values: [
            {
                initialFound: 1,
                found: 1,
                value: '2017',
                id: '14440317',
            },
        ],
        valuesGroups: [
            {
                type: 'all',
                valuesIds: [
                    '14440317',
                ],
            },
        ],
    },
];

<div>
    <SpecsTable filters={filters} />
</div>
```
