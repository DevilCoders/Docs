# Сущность "User"

Учётная запись пользователя на Маркете

### Поля:
  - uid `<Number>` - идентификатор пользователя
  - login `<String>` - логин пользователя
  - displayName `<String>` - отображаемое имя пользователя
  - firstName `<String>` - имя
  - lastName `<String>` - фамилия
  - avatarId `<String>` - определяющая часть веб-пути к аватару пользователя
  - defaultEmail `<String>` - адрес электронной почты

### Примеры:
```
"user": {
    "displayName": "spbtester",
    "uid": 67282295,
    "lastName": "Pupkin",
    "firstName": "Vasily",
    "login": "spbtester",
    "avatarId": "38436/67282295-936648932",
    "defaultEmail": "spbtester@yandex.ru"
}
```
