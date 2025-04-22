**Здесь описываем события относящиеся к Кошельку**


`CashbackCard.Shown` - показ дома Плюса (событие есть от старой карточки кэшбека)

Параметры:
* CommonParams
* open_reason - откуда открыли (TariffCard, OrderStatusNotification, Teaser, Menu, Deeplink, MenuPaymentMethodsPromo, SummaryPaymentMethodsPromo, OrderComplete, QR_payment)

**События апгрейда подписки со скидочной на кэшбэчную**

`CashbackCard.ActivationButtonTapped` - нажатие или перемещение активации кэшбека
Параметры:
* CommonParams

`CashbackCard.ActivationCashbackSuccess` - баллы активированны 

Параметры:
* CommonParams
       
`CashbackCard.ActivationCashbackFailed` - ошибка активации

Параметры:
* CommonParams

**События оплаты по QR**

`CashbackCard.PayAtTheCafeTapped` - нажатие на кнопку "заплатить в кафе"

Параметры:
* CommonParams
* open_reason - откуда зашли в Дом плюса

`CashbackCard.CafeWithCashbackTapped` - нажатие на кнопку "кафе с кэшбеком"

Параметры:
* CommonParams
* open_reason - откуда зашли в Дом плюса

**События покупки подписки в Доме плюса**

`CashbackCard.YandexPlusBuySubscriptionTapped` - нажатие на попробовать бесплатно  
Параметры:
* CommonParams
* open_reason - откуда зашли в Дом плюса 

`CashbackCard.YandexPlusBuySubscriptionSuccess` - успешная активация плюса 


Параметры:
* CommonParams
* open_reason - откуда зашли в Дом плюса

`CashbackCard.YandexPlusBuySubscriptionFailed` - ошибка активации 
Параметры:
* CommonParams
* open_reason - откуда зашли в Дом плюса

`CashbackCard.CompositePayment.Switсhed` - оплатить поездку в Доме плюса 
Параметры:
* CommonParams 
* swith_state - состояние свитча после переключения


`CashbackCard.PaySubscriptionByCashback.Switched` - свитч продлевать подписку баллами (в Доме плюса)

Параметры:
* CommonParams
* swith_state - состояние свитча после переключения

`CashbackCard.DetailsTapped` - нажатие на детали подписка

Параметры:
* CommonParams

       
**Бейдж кэшбэка в правом верхнем углу**

`Main.CashbackBadgeTapped` - нажатие на бейдж с кэшбеком 

Параметры:
* CommonParams
* mode - экран (main/summary/ride)
* Counter - число на каунтере

`Main.CashbackBadgeShown` - показ бейджа с кэшбеком 

Параметры:
* CommonParams
* mode - экран (main/summary/ride)
* Counter - число на каунтере

**Промо кэшбэка в методах оплаты**

`PaymentMethods.ActivationCashbakTapped` - нажатие на активацию кэшбека в способах оплаты (для перехода на баллы или подключения плюса)

Параметры:
* CommonParams
* has_subscription - true/false 


**Сториз**

`CashbackStories.ButtonTapped` - нажатие на кнопку в истории

Параметры:
* CommonParams
* open_reason - откуда открыли историю (пример push, cashbackcard, badge)
* number - порядковый номер ролика
* story_id - id истории
* number_total_count - общее число роликов
* story_position - порядковый номер истории в ленте

`CashbackStories.LoadingIndicatorAppeared`  - начало загрузки видео 

Параметры:
* CommonParams
* open_reason - откуда открыли историю (пример push, cashbackcard, badge)
* number - порядковый номер ролика
* story_id - id истории
* story_position - порядковый номер истории в ленте

`CashbackStories.LoadingIndicatorDisappeared` - окончание загрузки видео

Параметры:
* CommonParams
* open_reason - откуда открыли историю (пример push, cashbackcard, badge)
* number - порядковый номер ролика
* story_id - id истории
* story_position - порядковый номер истории в ленте
* success - проигрывание или нет, если историю закрыли, не дождавшись загрузки — отправляем false

`CashbackStories.PlayStarted` - начало воспроизведения истории 

Параметры:
* CommonParams
* open_reason - откуда открыли историю (пример push, cashbackcard, badge)
* number - порядковый номер ролика
* story_id - id истории
* number_total_count - общее число роликов
* story_position - порядковый номер истории в ленте

`CashbackStories.PlayFinished` - окончание воспроизведение истории

Параметры:
* CommonParams
* open_reason - откуда открыли историю (пример push, cashbackcard, badge)
* number - порядковый номер ролика
* story_id - id истории
* number_total_count - общее число роликов
* story_position - порядковый номер истории в ленте
* played_time - суммарное время ролика
* played_progress - сколько времени просмотрел пользователь



**Композитная оплата** 

`Menu.Payment.CashbackSwitch` - нажатие на Потратить на поездку

Параметры:
* CommonParams
* cashback_switch - состояние свитча Потратить на поездку on/off
* change_type - способ переключение свитча (пользователь / автоматически из-за несовместимого способа оплаты auto/user
* payment_method - выбранный способ оплаты НЕ КЭШБЕК (null/cash/card/applepay/googlepay)

`Menu.Payment.CashbackNotAvailable` - недоступность кешбека (когда свитч Потратить на поездку заблокирован и его состояние нельзя изменить), например, при выбора способа оплаты - наличными.

Параметры:
* CommonParams

`Menu.Payment.CashbackBubbleShown` - показ бабла в свитче

Параметры:
* CommonParams


`Summary.CompositePayment.Switсhed` - переключение на оплату баллами прям на саммари 

Параметры:
* CommonParams 
* swith_state - состояние свитча после переключения	

`Menu.CompositePayment.Switсhed` - переключение на оплату баллами прямо в меню

Параметры:
* CommonParams 
* swith_state - состояние свитча после переключения	



**Дефолтные события** 

`Map.PromoObject.Available` - доступность объекта на карте 

Параметры:
* CommonParams
* Mode - экран (main/summary/ride)

`Map.PromoObject.Shown` - показ объекта кэшбека на карте 

Параметры:
* CommonParams
* Mode - экран (main/summary/ride)
     
`Map.PromoObject.Tapped` - нажатие на объект кэшбека на карте 

Параметры:
* CommonParams
* Mode - экран (main/summary/ride)

`Main.SuggestCard.ButtonClicked` - нажатие на шорткат
