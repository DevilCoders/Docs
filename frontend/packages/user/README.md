#@yandex-lego/user

Компонент для работы с блоком пользователя.

```bash
# установка
npm i -PE @yandex-lego/user
```

## Подключение

```ts
import { User } from '@yandex-lego/user/desktop';

const const Header = () => (
    <header>
      <User />
    </header>
)
```

## Кастомизация 

### CSS-переменные
> Компонент использует CSS переменные, вы можете на удобный вам селектор (внутри которого лежит блок пользователя) добавлять следующие значения

| Токен                 |           Описание           |                Значение по умолчанию |
| --------------------- | :--------------------------: | -----------------------------------: |
| `--user-id-size`      |        Размер UserPic        |  _desktop_ **42px** _touch_ **22px** |
| `--user-id-size-plus` | Размер обводки Плюса UserPic | _desktop_ **52px**, _touch_ **30px** |


> следующие токены нужны, если вы используется withCounters, они управляют Badge компонентом 

| Токен                           |                            Значение по умолчанию |
| ------------------------------- | -----------------------------------------------: |
| `--user-id-badge-size`          |                                         **16px** |
| `--user-id-badge-font-size`     |                                         **12px** |
| `--user-id-badge-border-radius` |                                          **8px** |
| `--user-id-badge-border-width`  |                                          **2px** |
| `--user-id-badge-typo-color`    |                                         **#fff** |
| `--user-id-badge-fill-color`    |                                         **#f33** |
| `--user-id-badge-font-family`   | **Helvetica Neue, Helvetica, Arial, sans-serif** |
