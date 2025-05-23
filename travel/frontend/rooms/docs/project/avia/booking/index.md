# Avia. Book on Yandex

**Book on Yandex** (BoY) — бронирование и покупка авиабилетов в сервисе Яндекс.Путешествия.

-   [Спеки по дизайну](https://www.figma.com/file/GnNGpx3Mz3XvWZvVYjQXQyk6/Avia.-BoY?node-id=1%3A1655)

## Как попасть на BoY?

В данный момент BoY работает **только с Аэрофлотом**. Поэтому, чтобы попасть на бой,
нужно найти в поиске авиа вариант, который продаёт Аэрофлот. Для этого можно поискать
направление Москва — Екатеринбург в эконом классе и в фильтре партнёров выбрать "Аэрофлот".

<details><summary>Пример</summary>
<img src="serp-partner-filter.png" />
</details>

После нажатия, кнопки "Купить" должен произойти редирект на страницу BoY.
![boy-page](./boy-page.png)

> Исходный код страницы находится в папке `src/projects/avia/pages/AviaBooking`

Эта страница состоит из:

-   <details><summary>описание варианта</summary>
    <img src="boy-variant-info.png" />
    </details>
-   <details><summary>паспортные данные всех пассажиров</summary>
    <img src="boy-form-passport.png" />
    </details>
-   <details><summary>контактная информация покупателя</summary>
    <img src="boy-form-contacts.png" />
    </details>
-   <details><summary>блок выбора тарифа и кнопки оплаты</summary>
    <img src="boy-form-tariffs.png" />
    </details>

## Что происходит когда пользователь переходит на страницу?

URL страницы содержит в себе параметр `token`. При переходе на страницу
отправляется запрос с этим токеном в travel-api в метод `/avia_booking_flow/v1/variants`
за данными содержащими информацию о вариантах с тарифами.

После получения ответа отрисовывается страница.

![boy-loading](boy-loading.png)

Параллельно отправляется запрос в апи записной книжки путешественника для получения
интентов автозаполнения форм.

## Как забронировать билет?

### Выбор тарифа

API может вернуть несколько тарифов с различным набором опций, которые отобразяться в блоке выбора тарифа. Пользователь может выбрать интересующий его тариф. При этом информация в блоке описания варианта
будет обновляться в зависимости от выбранного тарифа.

В блоке выбора тарифа показывается не больше двух тарифов: текущий тариф и следующий более дорогой тариф (если он есть).

Все тарифы можно посмотреть, нажав на кнопку "Показать все тарифы".
После этого покажется всплывающее окно с отображением всех тарифов.

<details>
    <summary>Скрин</summary>
    ![boy-all-tariffs](boy-all-tariffs.png)
</details>

Если в этом окошке выбрать другой тариф, то блок выбора тарифа перерисуется и отобразит текущий и следующий более дорогой тариф (если он есть).

### Заполнение паспортных данных пассажиров и контактной информации покупателя.

В блоке паспортных данных пассажиров находится N форм, где N — число пассажиров. В каждую форму необходимо ввести паспортные данные каждого пассажира. В формах есть клиентская [валидация](####-Как-работает-клиентская-валидация?), которая помогает пользователям не совершать ошибок при заполнении форм и исключить отправку заведемо ошибочных запросов на бронирование билетов.

#### Как работает клиентская валидация?

Для валидации поля в форме могут быть в двух состояниях:

-   **pristine** — начальное состояние поля, с которым пользователь не взаимодействовал
-   **dirty** — поле, с которым взаимодействовал пользователь.

Для того, чтобы перешло из состояния **pristine** в **dirty** нужно зафокусить поле, а потом убрал фокус с этого поля.

![boy-pristine-dirty-switch](boy-pristine-dirty-switch.gif)

Второй способ — нажать по кнопке "**Оплатить**". В таком случае, все поля помечаются как **dirty**.

![boy-validation](boy-validation.gif)

Обратного перехода из состояни **dirty** в **pristine** нет.

Валидация отображается только в полях в состоянии **dirty**, и реагирует на каждое изменение поля, чтобы дать пользователю мгновенный фидбек. Если значение в поле проходит валидацию, то валидация мгновенно скрывается.

> Исходный код валидаций можно посмотреть в файле `src/projects/avia/pages/AviaBooking/lib/validatePassengerForm.ts`

## Бронирование авиабилетов

После того как форма заполнена правильно пользователь может забронировать билет нажав кнопку "Оплатить".

![boy-booking-flow](boy-booking-flow.png)

Далее отправляется запрос в API на создание заказа, в котором передаются паспортные данные пассажиров и контактные данные покупателя.

В ответ API присылает данные заказа, котором есть идентификатор — `orderId`. Клиент начинает полить API на статус заказа, до тех пор пока статус не будет финальным.

> Финальными статусами являются статус ошибки, или статус успеха

> После определённого таймаута, в API статус заказа атоматически переводится в ошибочное состония.

В зависимости от статуса заказа отображается различный интерфейс:

-   если `orderStatus == 'OS_WAIT_CARD_TOKENIZED'` и API прислало `paymentUrl`, то отображается форма траста: ![boy-trust](boy-trust.png)
-   после заполнения формы траста, банк может затребовать подтверждение оплаты в виде **3DS**. Страница 3DS отображется при получении `confirmationUrl` от API: ![boy-3ds](boy-3ds.png)

После получения финального статуса (или по таймауту) произойдёт редирект на страницу заказа.

Если статус заказа не является успешным, то показываем предупреждение: ![boy-order-failure](boy-order-failure.png)
