# Contacts

Компонент с формой контактов пользователя.

## Пример использования

```typescript jsx
import React, { useState } from 'react';

import { ContactsForm, Contacts } from '@yandex-int/tap-components/ContactsForm';

const App: React.FC = () => {
    const [contacts, setContacts] = useState<Contacts>({
        name: '',
        phone: '',
        email: ''
    });

    const onChange = (changes: Contacts) => {
        setContacts({ ...contacts, ...changes });
    };

    return (
        <ContactsForm
            contacts={contacts}
            onChange={onChange}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-contactsform--playground%}}

## Свойства

| Свойство   | Тип                            | Описание                                                                                     |
| ---------- | ------------------------------ | -------------------------------------------------------------------------------------------- |
| className? | `string`                       | Дополнительный класс у корневого DOM-элемента                                                |
| contacts   | `Contacts`                     | Данные контактов пользователя. Если поле внутри не указано, поле ввода не будет отображаться |
| onChange   | `(changes: Contacts) => void;` | Обработчик изменения формы. На вход принимает объект с измененной частью формы               |

```typescript jsx
type Contacts = {
    name?: string;
    phone?: string;
    email?: string;
};
```
