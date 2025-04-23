# Компонт с шапкой и навигацией страницы

Props:

| prop                    | type              | Описание                                                                    |
| ----------------------- | ----------------- | --------------------------------------------------------------------------- |
| tld                     | string            | TLD, например `ru`                                                          |
| lang                    | string            | Язык пользователя, например `en`                                            |
| pathname                | string            | Текущий pathname, например `/profile`                                       |
| isProfile?              | boolean           | Включается на главной странице профиля, меняет ссылку логотипа в шапке      |
| isHeaderHidden?         | boolean           | Скрывает шапку                                                              |
| navigationLinks         | INavLink[]        | Пункты навигации                                                            |
| specialNavigationLinks? | INavLink[]        | Специальные пункты под разделителем                                         |
| otherNavigationLinks?   | INavLink[]        | Дополнительные пункты под разделителем                                      |
| linkComponent?          | React.ElementType | Позволяет использовать свой компонент ссылки, например Link из react-router |
| user?                   | React.ReactNode   | Отображает переключатель аккаунтов                                          |
| plus?                   | React.ReactNode   | Отображает баланс Плюса                                                     |
