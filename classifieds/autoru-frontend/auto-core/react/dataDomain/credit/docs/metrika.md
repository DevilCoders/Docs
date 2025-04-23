### Префиксы страниц:
* Карточка авто - `cars/card/`
* Листинг - `cars/listing/`
* Кредитный раздел в личном кабинете - `my-credits/`
* Пункты меню в лк - `cars/sales/tabs/`
* (добавить главную)
* (добавить отчеты)

Финальный путь всех метрик складывается следующим образом: префикс страницы + путь самой метрики
Для примера, путь для открытия модала с короткой заявкой в листинге будет выглядеть так:
`cars/listing/credit-form-modal/show`

### Кредитный блок на карточке
* Состояние "Форма"
  * показ - `credit-card/form/show`
  * создание заявки - `credit-card/form/application-created`
  * остальные метрики лежат в форме
* Состояние "Прикрепить тачку"
  * показ - `credit-card/attach-car/show`
  * клик по кнопке "выбрать авто" - `credit-card/attach/attach-button-click`
  * успешное прикрепление тачки - `credit-card/attach-car/attach-success`
  * ошибка прикрепления тачки - `credit-card/attach-car/attach-error`
* Состояние "Заменить тачку"
  * показ - `credit-card/replace-car/show`
  * клик по кнопке "заменить" - `credit-card/replace-car/replace-button-click`
  * успешная замена тачки - `credit-card/replace-car/replace-success`
  * ошибка замены тачки - `credit-card/replace-car/replace-error`
  * клик по кнопке "продолжить" - `credit-card/replace-car/continue-button-click`
* Состояние "Продолжить"
  * показ - `credit-card/continue/show`
  * клик по кнопке - `credit-card/continue/continue-button-click`
* Состояние "Активная заявка"
  * показ - `credit-card/active/show`
  * клик по сниппету - `credit-card/active/snippet-click`
  * клик по ссылке ЛК - `credit-card/active/lk-link-click`
* Модал "Тачка прикреплена"
  * показ - `credit-card/attach-modal/show`
  * закрытие - `credit-card/attach-modal/closed`
  * клик по кнопке "продолжить" - `credit-card/attach-modal/continue-button-click`
* Модал "Тачка заменена"
  * показ - `credit-card/replace-modal/show`
  * закрытие - `credit-card/replace-modal/closed`
  * клик по кнопке "продолжить" - `credit-card/replace-modal/continue-button-click`

### Короткая кредитная заявка
* заявка создана/открыли визард - `credit-form/application-created`
* успешный сабмит - `credit-form/submit/success`
* сабмит с ошибкой валидации (любой, общий каунтер) - `credit-form/submit/validation-error`
* сабмит с ошибкой валидации почты - `credit-form/submit/validation-error`
* сабмит с ошибкой валидации ФИО - `credit-form/submit/validation-error`
* сабмит с непроставленным соглашением - `credit-form/submit/agreement-error`

### Модал с короткой кредитной заявкой
* открытие - `credit-form-modal/show`
* закрытие - `credit-form-modal/close`
* заявка создана - `credit-form-modal/application-created`

### Цена в кредит
* --клик и перевод в лк - `credit-price/click-to-lk`--
* клик и перевод на карточку авто, к блоку кредитов - `credit-price/click-to-card`
* клик и открытие кредитной формы в модале - `credit-price/click-to-form`
* клик и подскролл к блоку на карточке - `credit-price/click-to-scroll`

### Личный кабинет кредитов
* Состояние "Форма"
  * показ - `credit-lk/inactive/show`
  * создание заявки - `credit-lk/inactive/application-created`
* Состояние "Драфт"
  * показ - `credit-lk/draft/show`
* Состояние "Активная заявка"
  * показ - `credit-lk/active/show`
  * клик на кнопку/ссылку "редактировать" - `credit-lk/active/edit-click`
  * успешное добавление кредитного продукта - `credit-lk/active/add-product/success`
  * неуспешное добавление кредитного продукта - `credit-lk/active/add-product/error`
  * успешное удаление кредитного продукта - `credit-lk/active/delete-product/success`
  * неуспешное удаление кредитного продукта - `credit-lk/active/delete-product/error`
  * показ баннера "Эта машина продана" - `credit-lk/active/sold-banner/show`
  * клик на кнопку баннера "эта машина продана" - `credit-lk/active/sold-banner/button-click`
  * (пока нет) показ баннера "Дополни заявку" - `credit-lk/active/edit-banner/show`
  * (пока нет) клик на кнопку баннера "Дополни заявку" - `credit-lk/active/edit-banner/button-click`


### Провязка в галерее
* Состояние "Заполнить заявку"
  * показ - `credit-gallery/create/show`
  * клик по кнопке - `credit-gallery/create/button-click`
* Состояние "Прикрепить тачку"
  * показ - `credit-gallery/attach-car/show`
  * клик по кнопке "выбрать авто" - `credit-gallery/attach-car/button-click`
  * успешное прикрепление тачки - `credit-gallery/attach-car/attach-success`
  * ошибка прикрепления тачки - `credit-gallery/attach-car/attach-error`
* Состояние "Заменить тачку"
  * показ - `credit-gallery/replace-car/show`
  * клик по кнопке "заменить" - `credit-gallery/replace-car/button-click`
  * успешная замена тачки - `credit-gallery/replace-car/replace-success`
  * ошибка замены тачки - `credit-gallery/replace-car/replace-error`
* Состояние "Продолжить заполнение"
  * показ - `credit-gallery/continue/show`
  * клик по кнопке - `credit-gallery/continue/button-click`
* Состояние "Автомобиль заменен"
  * клик по кнопке "продолжить" - `credit-gallery/replaced/button-click`
* Состояние "Автомобиль прикреплен"
  * клик по кнопке "продолжить" - `credit-gallery/attached/button-click`

### Промо провязка
* Главная ЛК - `credit-promo-banner,lk-main-active,click`
* Визард десктоп - `credit-promo-banner,credit-wizard-desktop,click`
* Форма - `credit-promo-banner,credit-accordion,click`
* КЗ - `credit-promo-banner,credit-form2,click`
* Кредитный Флоу - `credit-promo-banner,credit-flow,${ flowView },click`, где flowView - состояние блока

### Динамическая провязка по рандомному продукту на карточке в таче
* клик и подскролл к блоку на карточке - `credit-dynamic-banner/click-to-scroll`

### Провязка в отчете
* Дефолтное состояние (заполни заявку)
  * показ - `credit-report/create/show`
  * клик - `credit-report/create/click`
* Состояние "Кредит почти ваш"
  * показ - `credit-report/continue/show`
  * клик - `credit-report/continue/click`

### Плитка на главной в таче
* Дефолтное состояние (заполни заявку)
  * показ - `credit-index-banner/create/show`
  * клик - `credit-index-banner/create/click`
* Состояние "Кредит почти ваш"
  * показ - `credit-index-banner/continue/show`
  * клик - `credit-index-banner/continue/click`
* Состояние "Есть заявка"
  * показ - `credit-index-banner/finish/show`
  * клик - `credit-index-banner/finish/click`

### Баннер-врезка на листинге
* Дефолтное состояние (заполни заявку)
  * показ - `credit-listing-banner/create/show`
  * клик - `credit-listing-banner/create/click`
* Состояние "Кредит почти ваш"
  * показ - `credit-listing-banner/continue/show`
  * клик - `credit-listing-banner/continue/click`


### Визард Мобильный
  * показ - `credit-wizard-mobile/show`
  * закрытие
    * клик на крестик - `credit-wizard-mobile/close/click`
    * подтверждение закрытия - `credit-wizard-mobile/close/aproove`
    * отказ от закрытия - `credit-wizard-mobile/close/cancel`
  * показ экрана
    * паспортные данные - `credit-wizard-mobile/show-step/passport`
    * менялась фамилия? - `credit-wizard-mobile/show-step/surname_changed`
    * старая фамилия - `credit-wizard-mobile/show-step/previous_surname`
    * адрес регистрации - `credit-wizard-mobile/show-step/registration_address`
    * адрес проживания другой? - `credit-wizard-mobile/show-step/residence_address_choose`
    * адрес проживания - `credit-wizard-mobile/show-step/residence_address`
    * кем работаю
      * выбор - `credit-wizard-mobile/show-step/employment_choose`
      * самозанятый
        * о компании - `credit-wizard-mobile/show-step/self_employment_about_company`
        * адрес - `credit-wizard-mobile/show-step/employment_address`
      * на компанию
        * данные о компании - `credit-wizard-mobile/show-step/employment_about_company`
        * должность - `credit-wizard-mobile/show-step/employment_position_type`
        * стаж - `credit-wizard-mobile/show-step/employment_last_experience`
        * адрес - `credit-wizard-mobile/show-step/employment_address`
      * безработный
        * причина бомжевания - `credit-wizard-mobile/show-step/not_employed_reason`
        * другая причина - `credit-wizard-mobile/show-step/not_employed_other_reason`
    * доход - `credit-wizard-mobile/show-step/income_monthly`
    * способ подтверждения дохода - `credit-wizard-mobile/show-step/income_proof`
    * доп персона
      * тип личности - `credit-wizard-mobile/show-step/related_person_type`
      * сам - `credit-wizard-mobile/show-step/related_person_self`
      * другой - `credit-wizard-mobile/show-step/related_person`
    * есть ли ВУ
      * выбор - `credit-wizard-mobile/show-step/driver_license`
      * своё ВУ - `credit-wizard-mobile/show-step/own_driver_license`
      * чужое ВУ - `credit-wizard-mobile/show-step/related_driver_license`
    * количество нахлебников - `credit-wizard-mobile/show-step/dependents`
    * контрольное слово - `credit-wizard-mobile/show-step/control_word`
    * выбор тачки - `credit-wizard-mobile/show-step/offer`
  * выбор тачки
    * клик по "выбрать авто" (нет прикрепленного) - неприменимо для мобилки
    * клик по "заменить авто" - неприменимо для мобилки
    * выбор из последних - `credit-wizard-mobile/offer-select/choose/last_car`
    * выбор из избранных - `credit-wizard-mobile/offer-select/choose/favorites`
    * показ пустых последних - `credit-wizard-mobile/offer-select/empty/last_car`
    * показ пустых избранных - `credit-wizard-mobile/offer-select/empty/favorites`
    * клик по "найду другой" - `credit-wizard-mobile/offer-select/find-another/click`
  * подтверждение ухода с визарда - `credit-wizard-mobile/offer-select/find-another/confirm`
  * отказ от ухода с визарда - `credit-wizard-mobile/offer-select/find-another/cancel`
  * ошибка сохранения от апи (нет интернета) - `credit-wizard-mobile/submit/save-error/no-result`
  * ошибка сохранения от апи (ошибка от сервера)- `credit-wizard-mobile/submit/save-error/action-error`
  * ошибка сохранения от апи (нету ok)- `credit-wizard-mobile/submit/save-error/not-ok`
  * ошибка сохранения от валидации - `credit-wizard-mobile/submit/save-error/validation`
  * ошибка саджеста в поле
    * кем выдан паспорт - `credit-wizard-mobile/suggest-error/passport_rf_depart_name`
    * место рождения - `credit-wizard-mobile/suggest-error/birth_place`
    * старая фамилия - `credit-wizard-mobile/suggest-error/old_name_surname`
    * адрес регистрации - `credit-wizard-mobile/suggest-error/registration_address`
    * адрес проживания - `credit-wizard-mobile/suggest-error/residence_address`
    * компания - `credit-wizard-mobile/suggest-error/self_employment_company`
    * компания - `credit-wizard-mobile/suggest-error/employment_company`
    * адрес компании - `credit-wizard-mobile/suggest-error/employment_address`

### Визард Десктопный
  * показ - `credit-wizard-desktop/show`
  * закрытие
    * клик на крестик - `credit-wizard-desktop/close/click`
    * подтверждение закрытия - `credit-wizard-desktop/close/aproove`
    * отказ от закрытия - `credit-wizard-desktop/close/cancel`
  * показ экрана -
    * выбор тачки и калькулятор - `credit-wizard-desktop/show-step/calculator_and_offer`
    * личные данные - `credit-wizard-desktop/show-step/profile`
    * паспортные данные - `credit-wizard-desktop/show-step/passport`
    * адрес - `credit-wizard-desktop/show-step/address`
    * место работы - `credit-wizard-desktop/show-step/employment`
    * доп персона - `credit-wizard-desktop/show-step/related_person`
    * ВУ - `credit-wizard-desktop/show-step/driver_license`
    * доп поля и галочки - `credit-wizard-desktop/show-step/additionals_and_agreements`
  * выбор тачки
    * клик по "выбрать авто" (нет прикрепленного) - `credit-wizard-desktop/offer-select/choose_car/click`
    * клик по "заменить авто" - `credit-wizard-desktop/offer-select/change_car/click`
    * выбор из последних - `credit-wizard-desktop/offer-select/choose/last_car`
    * выбор из избранных - `credit-wizard-desktop/offer-select/choose/favorites`
    * клик по "найду другой" - `credit-wizard-desktop/offer-select/find-another/click`
    * подтверждение ухода с визарда - `credit-wizard-desktop/offer-select/find-another/confirm`
    * отказ от ухода с визарда - `credit-wizard-desktop/offer-select/find-another/cancel`
  * ошибка сохранения от апи (нет интернета) - `credit-wizard-desktop/submit/save-error/no-result`
  * ошибка сохранения от апи (ошибка от сервера)- `credit-wizard-desktop/submit/save-error/action-error`
  * ошибка сохранения от апи (нету ok)- `credit-wizard-desktop/submit/save-error/not-ok`
  * ошибка авто сохранения от апи (ошибка от сервера)- `credit-wizard-desktop/auto-save/save-error/action-error`
  * ошибка авто сохранения от апи (нету ok)- `credit-wizard-desktop/auto-save/save-error/not-ok`
  * ошибка сохранения от валидации - `credit-wizard-desktop/submit/save-error/validation`
  * ошибка саджеста в поле
    * кем выдан паспорт - `credit-wizard-desktop/suggest-error/passport_rf_depart_name`
    * место рождения - `credit-wizard-desktop/suggest-error/birth_place`
    * старая фамилия - `credit-wizard-desktop/suggest-error/old_name_surname`
    * адрес регистрации - `credit-wizard-desktop/suggest-error/registration_address`
    * адрес проживания - `credit-wizard-desktop/suggest-error/residence_address`
    * компания - `credit-wizard-desktop/suggest-error/self_employment_company`
    * компания - `credit-wizard-desktop/suggest-error/employment_company`
    * адрес компании - `credit-wizard-desktop/suggest-error/employment_address`


### Большая форма
* Показ полной формы `credit-accordion/show`
    После визарда `credit-accordion/show/from-wizard`
    На редактирование (любое открытие, кроме визарда) credit-accordion/show/from-edit`

* Клик по кнопке Отправить (=отправить полную форму)
    * Успех (=перешла из DRAFT  в статус NEW) `credit-accordion/submit/success`
    * Ошибка, поля невалидны `credit-accordion/submit/validation-error`
	* Ошибка, нет согласия отправки Банкам `credit-accordion/submit/agreement-error`

* Блок выбора автомобиля
    * Клик на ссылку прикрепленного оффера `credit-accordion/chosen-offer-link/click`

    * Клик по кнопке Заменить авто (=Изменить авто) `credit-accordion/offer-section-with-offer/change-car/click`
    * клик на объект в Последних `credit-accordion/offer-section-with-offer/recent/click`
    * клик на объект в Избранных `credit-accordion/offer-section-with-offer/favorite/click`
    * открытие блока выбора автомобиля без объявлений (сразу с кнопкой Найду другой) `credit-accordion/offer-section-with-offer/find-another/show`
    * клик на кнопку Найду другой `credit-accordion/offer-section-with-offer/find-another/click`
    * подтвердил уход с формы `credit-accordion/offer-section-with-offer/find-another/confirm`
    * отказался уходить с формы `credit-accordion/offer-section-with-offer/find-another/cancel`

    * показ экрана выбора тачки без Последних `credit-choose-car/no-recent-offers`
    * показ экрана выбора тачки без Избранных `credit-choose-car/no-favorite-offers`

    * Клик на кнопку Выбрать автомобиль // авто не прикреплен `credit-accordion/offer-section-without-offer/change-car/click`
    * клик на объект в Последних `credit-accordion/offer-section-without-offer/recent/click`
    * клик на объект в Избранных `credit-accordion/offer-section-without-offer/favorite/click`
    * открытие блока выбора автомобиля без объявлений (сразу с кнопкой Найду другой) `credit-accordion/offer-section-without-offer/find-another/show`
    * клик на кнопку Найду другой `credit-accordion/offer-section-without-offer/find-another/click`
    * подтвердил уход с формы `credit-accordion/offer-section-without-offer/find-another/confirm`
    * отказался уходить с формы `credit-accordion/offer-section-without-offer/find-another/cancel`


* Ошибка отправки
    * бэк вернул ошибку публикации `credit-accordion/publication-error/not-ok`
    * ошибка на каком-то из промежуточных шагов `credit-accordion/publication-error/action-error`
    * неведомая херня `credit-accordion/publication-error/unknown`

* Ошибка сохранения
    * бэк вернул ошибку сохранения `credit-accordion/save-error/not-ok`
    * ошибка на каком-то из промежуточных шагов `credit-accordion/save-error/action-error`
    * неведомая херня `credit-accordion/save-error/unknown`

* Ошибка ответа саджеста
    [тип] // например, Адрес регистрации
