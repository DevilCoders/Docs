# change-status-select

## Usage

### BEMJSON
```javascript
{
    block: 'change-status-select',
    mods: {
        width: 'available'
    },
    js: {
        taskId: 42474,
        requestId: 211219
    },
    isLastAttempt: false,
    status: {
        status: 'act_attributes'
    },
    content: [
        {
            block: 'select',
            mods: {
                mode: 'radio',
                theme: 'islands',
                size: 's',
                width: 'available'
            },
            js: {
                isLastAttempt: false
            },
            val: 'act_attributes',
            options: [
                {
                    val: 'act_attributes',
                    text: 'Акт. атрибутов',
                    disabled: false
                },
                {
                    val: 'act_full',
                    text: 'Актуализация',
                    disabled: false
                }
                {
                    val: 'missed_call',
                    text: 'Недозвон',
                    disabled: false
                },
                {
                    val: 'recall',
                    text: 'Перезвон',
                    disabled: false
                },
                {
                    val: 'can_not_process',
                    text: 'Не подлежит актуализации',
                    disabled: false
                },
                {
                    val: 'no_data',
                    text: 'Недостаточно данных',
                    disabled: false
                },
                {
                    val: 'duplicate',
                    text: 'Дубль',
                    disabled: false
                }
            ]
        },

        // блоки change-status-dialog для всех статусов

    ]
}
```
