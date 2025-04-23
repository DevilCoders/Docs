#b-edit-phrase-price-stat-popup#

##Описание##
Кнопка, открывающая попап, через который можно установить ставку для фразы (или группы фраз)

###Мейнтейнеры###
[skywhale](https://staff.yandex-team.ru/skywhale )
[grimfrid](https://staff.yandex-team.ru/grimfrid )

###Где используется###
В статистике, добавление ДРФ в группу (b-stat-phrases-manager, b-edit-phrase-price)

### Модификаторы ###
- multiedit_yes - установка единой цены для всех моделей
- justify - кнопка будет занимать всю доступную ширину

###Взаимодействие с другими блоками###
Тригеррит события show и hide при открытии/закрытии попапа

##Как пользоваться и расширять##
Добавить блок в нужное место и установить через метод initModels модель/модели для которых будет
устанавливаться цена

##Roadmap & known issues##
-

##Пример##

```
    {
        block: 'b-edit-phrase-price-stat-popup',
        js: {
            currency: 'RUB',
            campaign: {} // передается в b-phrases-auction-popup
        },
        price: '224.9',
        price_context: '0.3'
    }

```
