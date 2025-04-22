# Dialog

Диалоговое окно

Стандартное диалоговое модальное окно, которое появляется с затемнением фона.
Может отображаться с разным набором кнопок:
* одна активная (для call-to-action) - `OK_ACTIVE`
* две обычные (для диалога "Да/Нет") -  `YES_NO`
* одна обычная и одна псевдокнопка (для диалога удаления) - `CANCEL_REMOVE`

Пример использования:
```javascript
const {OK_ACTIVE} = require('@self/platform/components/Dialog');

const CustomDialog = () => (
    <Dialog
        buttons={OK_ACTIVE}
        isOpen={true}
        title="Жалоба на ответ"
        submitButtonText="Отправить"
        onSubmit={() => console.log('submit')}
        onClose={() => console.log('close')}
    >
        Содержимое окна
    </Dialog>
);

<CustomDialog />
```
