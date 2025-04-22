# Сущность "StaffUser"

Информация о сотруднике Яндекса со стаффа

### Поля:
  - **firstName** `<String>` - имя
  - **lastName** `<String>` - фамилия
  - **photoUrl** `<String>` - публично-доступный URL-адрес аватара
  - **email** `<String>` - адрес электронной почты
  - phone `<Object>` - телефон
    - **officeNumber** `<String>` - номер офиса
    - **personNumber** `<String>` - добавочный номер сотрудника
  - **active** `<Boolean>` - флаг активности (не-уволенности) сотрудника

### Примечания
- Если у юзера нет номера офиса ИЛИ персонального рабочего номера - поле `phone`
не будет прислано вообще. Пример: роботы или надомники.

### Примеры:
```
{
    "firstName": "Дарья",
    "lastName": "Новикова",
    "photoUrl": "https://s3.mdst.yandex.net/vendors-public/manager-avatars/yadaxa.jpg"
    "email": "yadaxa@yandex-team.ru",
    "phone": {
        "officeNumber": "+7 495 739-70-00",
        "personNumber": "2459"
    },
    "active": true,
}
```
```
{
    "firstName": "Vendors",
    "lastName": "Manager",
    "photoUrl": "https://s3.mdst.yandex.net/vendors-public/manager-avatars/robot-vendorsmanager.jpg"
    "email": "robot-vendorsmanager@yandex-team.ru",
    "active": true,
}
```