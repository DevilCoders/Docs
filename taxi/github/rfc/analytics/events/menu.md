**Здесь описываем события относящиеся к меню**

### История заказов 
`OrderHistory.Shown` - показ истории заказов 
* CommonParams
* open_reason - откуда был вызван элемент 
    * menu - из меню
    * в будущем возможен заход из кэшбека и еще каких-то мест
* timeSinceAppLaunch 

В событие `Menu.OrderHistoryTapped` добавить параметр `timeSinceAppLaunch`

`OrderHistory.FiltersTapped` - нажатие на фильтры в истории заказов
Параметры:
* CommonParams

`OrderHistory.OrderTapped` - нажатие на заказ в истории заказов 
Параметры:
* CommonParams 
* order_id - id заказа
* service - eda/taxi/groceru

`OrderHistory.FiltersCard.Switched` - нажатие на фильтры в истории заказов
Параметры:
* CommonParams
* switch_name - название свитча
* switch_state - состояние после 

`OrderHistory.OrderCard.Tapped` - нажатие на кнопки внутри заказа
Параметры:
* CommonParams
* order_id - id заказа
* service - taxi/grocery/eats
* button_name:
    * call_to_driver - cвязь с водителем
    * help_with_trip - помощь с поездкой
    * repeat_order - повторить заказ
    * check - чек
    * remove_order - удалить заказ
    * partner - перевозчик и партнер


`OrderHistory.HelpWithTrip.Tapped` - нажатие на кнопки помощи с поездков
Параметры:
* CommonParams
* button_name:
   * other_trip - другая поездка
   * problem_with_trip - проблемы с поездкой
   * problem_with_app - проблемы с приложением

`OrderHistory.Check.Tapped` - нажатие на кнопку внутри чека
Параметры:
* CommonParams
* button_name - share