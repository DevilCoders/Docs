# Менеджерские ручки
Ключ в стейте `vendorsManager`
В стейте хранятся значения по умолчанию, каждое значение можно переопределить путем добавления их в стейт.

**Данные в стейте**
```(js)
    firstName: 'Vendors',
    lastName: 'Manager',
    photoUrl: 'https://s3.mdst.yandex.net/vendors-public/manager-avatars/robot-vendorsmanager.jpg',
    email: 'manager@yandex-team.ru',
    active: true,
```


## GET `/vendors/<vendorId>/manager`
Получение информации о менеджере вендора

Всегда возвращает успешный ответ.

## PUT `/vendors/<vendorId>/manager`
Назначение текущего пользователя менеджером карточки вендора

Возвращает значение стейта по умолчанию.

## DELETE `/vendors/<vendorId>/manager`
Передача управления карточкой вендора в службу поддержки (саппорту)

### Ответ
- **meta** `<Object>`
- result `<Object>`
    - **item**
      - **removed** `<Boolean>` - признак успешности удаления
- errors `<Error[]>`
