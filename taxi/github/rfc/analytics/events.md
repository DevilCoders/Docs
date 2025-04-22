
**Экран рефералки:**

`Referral.Shown` - появление экрана рефералки
Параметры:
* CommonParams 
    * service = grocery - сервис рефералки, пробрасывается из ответа getreferral
    * rides_left - остаток промокодов
        *   open_reason = promo_object / superapp_shortcut / lavka_shortcut / transporting_button / lavka_order - из-за чего появился элемент/Откуда открылась карточка - отправляем пустым, пока не появился обработчик диплинков
        *   button_list = [share, actionbutton, cancel (крестик)] - список кнопок - actionbutton отправляем пока на бэке не реализуют аналитической название


**Экран рефералки 2**
`Referral.Shown` - появление экрана рефералки
Параметры:
* CommonParams 
    * service = grocery - сервис рефералки, пробрасывается из ответа getreferral
    * rides_left - остаток промокодов
        *   open_reason = promo_object / superapp_shortcut / lavka_shortcut / transporting_button / lavka_order - из-за чего появился элемент/Откуда открылась карточка - отправляем пустым, пока не появился обработчик диплинков
        *   button_list = [share, actionbutton, cancel (крестик)] - список кнопок - actionbutton отправляем пока на бэке не реализуют аналитической название