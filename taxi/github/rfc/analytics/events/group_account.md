==== Точки входа

__**Пуш (если аккаунт заведен в вебе)**__

##GroupAccountPush.Shown## - пуш получен
Параметры:
    * state - состояние элемента
      * family/business
    * CommonParams

__**Пункт в меню**__
Есть события
##Menu.TeamAccountTapped## - iOS
##SettingsDidSelectSelectGroup## - Android

__**Способ оплаты**__
Есть события
##PaymentMethodSelectionDidSelectFamilyAccount## - iOS
##payment_method.family_account## - Android

__**Из саммари Доставки**__
Добавить событие ##Summary.SummaryCard.GroupAccountTapped## - нажатие на кнопку "Подключить доставку для бизнеса" (событие старого формата)
Параметры:
    * tariff - тариф
    * state - состояние элемента
      * family/business
    * CommonParams


==== Новый флоу группового аккаунта

__**Сториз**__

##BusinessAccountStories.LoadingIndicatorAppeared## - Начало загрузки сториз
Параметры:
    * open_reason - откуда открыли историю
      * push/menu/payment/delivery
    * number - порядковый номер ролика
    * story_id - id истории
    * story_position - порядковый номер истории в ленте
    * CommonParams 
 
##BusinessAccountStories.LoadingIndicatorDisappeared## - Конец загрузки сториз 
Параметры:
    * open_reason - откуда открыли историю
      * push/menu/payment/delivery
    * number - порядковый номер ролика
    * story_id - id истории
    * story_position - порядковый номер истории в ленте
    * success - началось проигрывание или нет, если историю закрыли, не дождавшись загрузки — отправляем false
    * CommonParams
 
##BusinessAccountStories.PlayStarted## - Начало воспроизведения истории (Срабатывает в момент начала проигрывания, а не открытия истории)
Параметры:
    * open_reason - откуда открыли историю
      * push/menu/payment/delivery
    * number - порядковый номер ролика
    * story_id - id истории
    * number_total_count - общее число роликов
    * story_position - порядковый номер истории в ленте
    * CommonParams
 
##BusinessAccountStories.PlayFinished## - Конец воспроизведения истории (Срабатывает в момент окончания проигрывания.) Т.е. либо уходим на другой ролик/историю, либо закрываем плеер.
Параметры:
    * open_reason - откуда открыли историю
      * push/menu/payment/delivery
    * number - порядковый номер ролика
    * story_id - id истории
    * number_total_count - общее число роликов
    * story_position - порядковый номер истории в ленте
    * played_time - суммарное время ролика
    * played_progress - сколько времени просмотрел пользователь
    * CommonParams
 
##BusinessAccountStories.ButtonTapped## - Нажатие на кнопку в истории
Параметры:
    * open_reason - откуда открыли историю
      * push/menu/payment/delivery
    * number - порядковый номер ролика
    * story_id - id истории
    * number_total_count - общее число роликов
    * story_position - порядковый номер истории в ленте
    * CommonParams


__**Экран группового аккаунта**__

##CreateGroupAccount.Shown## - экран создания группового аккаунта
Параметры:
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент 
      * menu/payment_menu/payment_summary/delivery
    * CommonParams 

##GroupAccount.Shown## - открытие экрана группового аккаунта
Параметры:
    * group_id - id аккаунта
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент 
      * menu/payment_menu/payment_summary/delivery
    * button_list - список кнопок на элементе
      * back/card/mail/add_participants/promo/big_company/settings/action_button
    * CommonParams 
 
##GroupAccount.Tapped## - тап на кнопку на экране группового аккаунта
Параметры:
    * group_id - id аккаунта
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент
      * menu/payment_menu/payment_summary/delivery
    * button_list - список кнопок на элементе
      * back/card/mail/add_participants/promo/big_company/settings/action_button
    * button_name - название кнопки, которую нажали
      * back/out_screen/card/mail/add_participants/promo/big_company/settings/action_button
    * CommonParams


__**Приглашение участников**__
**iOS**

##GroupAccountParticipants.Shown## - открытие экрана "Пригласить участника"
Параметры:
    * group_id - id аккаунта
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент (откуда перешли)
      * group_account_screen/participants_list_card/limits_card
    * button_list - список кнопок на элементе
      * action_button/back/participant_selected
    * CommonParams
 
##GroupAccountParticipants.Tapped## - нажатие на кнопку на экране "Пригласить участника"
Параметры:
    * group_id - id аккаунта
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент
      * group_account_screen/participants_list_card/limits_card
    * button_list - список кнопок на элементе
      * action_button/back/participant_selected
    * button_name - название кнопки, которую нажали
      * done/back/participant_selected
    * CommonParams

**Android**

##GroupAccountParticipants.Shown## - открытие экрана "Пригласить участника"
Параметры:
    * group_id - id аккаунта
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент (откуда перешли)
      * group_account_screen/participants_list_card/limits_card
    * button_list - список кнопок на элементе
      * done/action_button/back/name/phone/from_contacts
    * CommonParams
 
##GroupAccountParticipants.Tapped## - нажатие на кнопку на экране "Пригласить участника"
Параметры:
    * group_id - id аккаунта
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент
      * group_account_screen/participants_list_card/limits_card
    * button_list - список кнопок на элементе
      * done/action_button/back/name/phone/from_contacts
    * button_name - название кнопки, которую нажали
      * done/action_button/back/name/phone/from_contacts
    * CommonParams

__**Алерт "Зачем добавлять коллег"**__

##GroupAccountParticipantsAlert.Shown## - показ алерта "Зачем добавлять коллег"
Параметры:
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент
      * group_account_screen/participants_list_card/limits_card
    * button_list - список кнопок на элементе
      * done
    * CommonParams

##GroupAccountParticipantsAlert.Closed## - закрытие алерта "Зачем добавлять коллег"
Параметры:
    * state - состояние элемента
      * family/business
    * close_reason - из-за чего скрылся элемент
      * done_button/android_back_button/out_alert/error
    * open_reason - из-за чего появился элемент
      * group_account_screen/participants_list_card/limits_card
    * button_list - список кнопок на элементе
      * done
    * CommonParams

##GroupAccountParticipantsAlert.Tapped## - нажатие на кнопку в алерте "Зачем добавлять коллег"
Параметры:
    * state - состояние элемента
      * family/business
    * open_reason - из-за чего появился элемент
      * group_account_screen/participants_list_card/limits_card
    * button_list - список кнопок на элементе
      * done
    * button_name - название кнопки
      * done
    * CommonParams


__**Карточка "Список коллег"**__
**iOS**

##GroupAccountParticipantsListCard.Shown## - показ карточки "Список коллег"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
      * group_account_screen/participants_screen/old_onboarding_screen
    * button_list - список кнопок на элементе
      * done/back/edit/card/participant_selected/add_participant
    * state - состояние элемента
      * family/business
    * CommonParams
 
##GroupAccountParticipantsListCard.Tapped## - тап на кнопку в карточке "Список коллег"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
      * group_account_screen/participants_screen/old_onboarding_screen
    * button_list - список кнопок на элементе
      * done/back/edit/card/participant_selected/add_participant
    * button_name - название кнопки, которую нажали
      * done/back/edit/card/participant_selected/add_participant
    * state - состояние элемента
      * family/business
    * CommonParams

##GroupAccountParticipantsListCard.Closed## - закртие карточки "Список коллег"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
      * group_account_screen/participants_screen/old_onboarding_screen
    * close_reason - из-за чего скрылся элемент
      * done/back/card/participant_selected/add_participant/out_card (тап вне области карточки)
    * button_list - список кнопок на элементе
      * done/back/edit/card/participant_selected/add_participant
    * state - состояние элемента
      * family/business
    * CommonParams

**Android**

##GroupAccountParticipantsListCard.Shown## - показ карточки "Список коллег"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
      * group_account_screen/old_onboarding_screen
    * button_list - список кнопок на элементе
      * done/back/edit/participant_deleted/participant_selected/add_participant
    * state - состояние элемента
      * family/business
    * CommonParams
 
##GroupAccountParticipantsListCard.Tapped## - тап на кнопку в карточке "Список коллег"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
      * group_account_screen/old_onboarding_screen
    * button_list - список кнопок на элементе
      * done/back/participant_selected/add_participant
    * button_name - название кнопки, которую нажали
      * done/back/edit/participant_deleted/participant_selected/add_participant
    * state - состояние элемента
      * family/business
    * CommonParams

##GroupAccountParticipantsListCard.Closed## - закртие карточки "Список коллег"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
      * group_account_screen/old_onboarding_screen
    * close_reason - из-за чего скрылся элемент
      * done/back/participant_selected/add_participant/out_card (тап вне области карточки)
    * button_list - список кнопок на элементе
      * back/edit/participant_deleted/participant_selected/add_participant
    * state - состояние элемента
      * family/business
    * CommonParams


__**Карточка настроек БА**__

##GroupAccountSettingsCard.Shown## - показ карточки настроек группового аккаунта
Параметры:
    * button_list - список кнопок на элементе
      * back/account_name/email_address/limit/delete_account
    * state - состояние элемента
      * family/business
    * CommonParams
 
##GroupAccountSettingsCard.Tapped## - тап на кнопку в карточке настроек группового аккаунта
Параметры:
    * button_list - список кнопок на элементе
      * back/email_address/limit/delete_account
    * button_name - название кнопки, которую нажали
      * back/email_address/limit/delete_account
    * state - состояние элемента
      * family/business
    * CommonParams


__**Лимиты на месяц**__

##MonthLimitsCurrencyCard.Shown## - открытие карточки "Лимиты на месяц", выбор валюты
Параметры:
    * button_list - список кнопок на элементе
      * done/back/currency_selected
    * CommonParams

##MonthLimitsCurrencyCard.Tapped## - нажатие на кнопку в карточке "Лимиты на месяц", выбор валюты
Параметры:
    * button_list - список кнопок на элементе
      * done/back/currency_selected
    * button_name - название кнопки, которую нажали
      * done/back/currency_selected
    * CommonParams

##MonthLimitsCard.Shown## - открытие карточки "Лимиты на месяц"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
      * participant_card/settings
    * button_list - список кнопок на элементе
      * done/back/user_selected
    * CommonParams

##MonthLimitsCard.Tapped## - нажатие на кнопку в карточке "Лимиты на месяц"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
      * participant_card/settings
    * button_list - список кнопок на элементе
      * done/back/user_selected
    * button_name - название кнопки, которую нажали
      * done/back/user_selected
    * CommonParams


__**Карточка "Коллега"**__

##GroupAccountParticipantCard.Shown## - открытие карточки "Коллега"
Параметры:
    * open_reason - из-за чего появился элемент
      * limits_card/participants_list_card
    * button_list - список кнопок на элементе
      * done/back/delete/name/phone/set_limit/limit_value
    * state - состояние элемента
      * family/business
    * CommonParams

##GroupAccountParticipantCard.Tapped## - нажатие на кнопку в карточке "Коллега"
Параметры:
    * open_reason - из-за чего появился элемент
      * limits_card/participants_list_card
    * button_list - список кнопок на элементе
      * done/back/delete/name/phone/set_limit/limit_value
    * button_name - название кнопки, которую нажали
      * done/back/delete/name/phone/set_limit/limit_value
    * state - состояние элемента
      * family/business
    * CommonParams


__**Алерт "Поменять у тех, кто уже с лимитом?"**__

##MonthLimitsAlert.Shown## - показ алерта "Поменять у тех, кто уже с лимитом?"
Параметры:
    * button_list - список кнопок на элементе
      * no/yes
    * CommonParams
 
##MonthLimitsAlert.Closed## - закрытие алерта "Поменять у тех, кто уже с лимитом?"
Параметры:
    * close_reason - из-за чего скрылся элемент
      * done_button/no_button/android_back_button/out_alert/error
    * button_list - список кнопок на элементе
      * no/yes
    * CommonParams
 
##MonthLimitsAlert.Tapped## - нажатие на кнопку в алерте "Поменять у тех, кто уже с лимитом?"
Параметры:
    * open_reason - из-за чего появился элемент/Откуда открылась карточка
    * button_list - список кнопок на элементе
      * no/yes
    * button_name - название кнопки
      * no/yes
    * CommonParams


__**Отчеты на почту**__

##ExpenditureReportCard.Shown## - открытие карточки "Отчеты о тратах"
Параметры:
    * button_list - список кнопок на элементе
      * done/back/email_address/frequency_selected
    * CommonParams

##ExpenditureReportCard.Tapped## - нажатие на кнопку в карточке "Отчеты о тратах"
Параметры:
    * button_list - список кнопок на элементе
      * done/back/email_address/frequency_selected
    * button_name - название кнопки, которую нажали
      * done/back/email_address/frequency_selected
    * CommonParams