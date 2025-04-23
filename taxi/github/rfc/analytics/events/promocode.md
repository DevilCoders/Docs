**Здесь описываем события относящиеся к скидкам**

**Экран Скидки**

`Menu.PromoCodeTapped` - Нажатие на "Скидка" в меню
Параметры:
* rating – рейтинг пользователя
* photo_flg: true/false – наличие фото
* user_name_flg: true/false - наличие имени

`PromoCodes.Shown` - Появилось окно с промокодами
Параметры:
* CommonParams
* promocodes = {'taxi':'2', 'eda':'3', 'grocery':null} - структура типа yson {сервис : кол-во промокодов}
* open_reason = menu/deeplink - откуда открылась карточка

`PromoCodes.Tapped` - Тап на элементы в карточке Скидки
Параметры:
* CommonParams
* service - для какого сервиса рефералка, пробрасывается из ответа getreferral, при отсутствии поля отправляется taxi
* button_name = invite_friend/promocode_details/delete/get_discount/enter_promocode (Пригласить друга/Промокод из списка/Удалить/Получить скидку/Ввести промокод) - название кнопки, на которую тапнули
* promocode - значение промокода (посылаем параметр в случае тапа на конкретный промокод)

`PromoCodes.Deleted` - Получили ответ от ручки удаления промокода
Параметры:
* CommonParams
* result = success/failure - результат удаления
* service = taxi/eda/grocery
* promocode - значение промокода

**Экран Ввести промокод**

Для событий ниже сделать одинаковые названия для Android и iOS!

`EnterPromoCodeCard.Shown` - Появилось окно ввод промокода 
Параметр:
* CommonParams
* type_error - тип ошибки

`EnterPromoCodeCard.CodeDeleted` - Стерли промокод (крестик ввода)
Параметр:
* CommonParams
* type_error - тип ошибки, который был

`EnterPromoCodeCard.ActivateButtonTapped` - Нажали кнопку активировать
Параметр:
* CommonParams
* type_error - тип ошибки
* is_empty = true/false - был ли пустой ввод

`EnterPromoCodeCard.Closed` - Закрыли окно с вводом промокода
Параметр:
* CommonParams
* type_error - тип ошибки
* close_reason = cancel/back_button (Отмена/Назад на Андроид) - из-за чего скрылся элемент

`EnterPromoCodeCard.Activated` - Получили ответ от ручки активации промокода
Параметр:
* CommonParams
* type_error - тип ошибки
* service = taxi/eda/grocery
* state = active/restriction/invalid active - состояние промокода
* promocode - значение промокода

**Добавить параметры service = taxi/eda/grocery, state = active/no_active и promocode в:**

`DiscountDescriptionCard.Shown` - Появилась карточка детали скидки
`DiscountDescriptionCard.Dismiss` - Скрыли детали
`DiscountDescriptionCard.ButtonTapped` - Нажали на кнопку на карточке
`CouponRequiresAddCardShown` - Показана кнопка "Добавить карту"
`CouponRequiresAddCardClicked` - Клик по кнопке "Добавить карту"
`CouponRequiresChangePaymentTypeShown` - Показана кнопка "Выбрать оплату другим способом"
`CouponRequiresChangePaymentTypeClicked` - Клик по кнопке "Выбрать оплату другим способом"