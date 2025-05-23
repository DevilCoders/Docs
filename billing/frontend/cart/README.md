# balance-cart
# Корзина
https://wiki.yandex-team.ru/billing/hr/bootcamp/tasks/cart-frame/

Корзина предназначена для встраивания в страницы сторонних сервисов с предоставлением возможности доступа к состоянию корзины биллинга с его визаулизацией,  добавлению в корзину новых позиций и перенеправления на страницу корзины.

### Корзина остоит из двух частей:
1. HTML-страницы, встраивающейся в клиентский сайт с помощью тега `<iframe>` (далее "`<iframe>`", "фрейм");
2. клиентской части - JavaScript кода, запускающегося на стороне сервиса.
Общение между составными частями Корзины происходит посредством стандартного [`postMessage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage).

### Добавление Корзины на сайт клиента.
Для добавления Корзины на сайт клиента необходимо:
1. создать на сайте клиента `<iframe>` - элемент, в который будет встроена HTML-страница Корзины;
2. добавить в конец тега `<head>` приведенный ниже код;
3. Вызвать `window.createBillingCart()` с парамтером объекта конфигурации с полями:
    `selector` - селектор, по которому можно найти `<iframe>`;
    `src` - URL-путь Корзины на хосте биллинга.

См. [пример работы с фреймом](src/widget/index.js)

 *Примечание 1*: sandbox-атрибут `<iframe>` автоматически будут выставлены следующие разрешения:
    `allow-same-origin allow-scripts allow-top-navigation-by-user-activation`.

 *Примечание 2*: минимально рекомендуемый размер `<iframe>`: 
 `{
     min-width: 28px;
     min-height: 28px;
 }`.

### Использование Корзины.
После добавления JavaScript-кода на странице клиента и вызова `window.createBillingCart()`, в глобальной области видимости создается объект window.yb, предоставляющий API для общения с фреймом со следующими методами:
1. `window.yb.addItem(qty, old_qty, service_id, service_order_id, payload)`
    добавляет позиции в Корзину, параметры задаются согласно [документу](https://wiki.yandex-team.ru/billing/hr/bootcamp/tasks/cart-frame/);
2. `window.yb.addHandler(handler)`
    добавляет обработчик сообщений, пришедших от Корзины, в качестве параметра которого при вызове передается объект сообщения согласно [документу](https://wiki.yandex-team.ru/billing/hr/bootcamp/tasks/cart-frame/);
3. `window.yb.removeHandler(handler)`
    удаляет обработчик сообщений;
4. `window.yb.isConnected()`
    возвращает булевое значение, показывающее, готова ли Корзина к работе в текущий момент.

Переход на страницу Корзины после добавления всех необходимых позиций осуществляется кликом мыши на фрейм.

### Последовательность работы Корзины:
1. **инициализация встраиваемого кода**: встраиваемый у клиента скрипт после вызова `window.createBillingCart()` создает и инициализирует объект `window.yb`, после чего задает фрейму атрибут src, инициируя в нем загрузку страницы Корзины;

2. **инициализация фрейма**: страница Корзины во фрейме загружается (при этом пока остается скрытой), находящийся на ее стороне JavaScript-код инициализируется и посылает на сервер биллинга запрос на текущее состояние корзины с помощью **GET**-метода `/cart/item/list`;

3. **получение статуса сервера**: возможны два варианта:
    * в случае, если сервер отвечает кодом ошибки **404** (сервису запрещено встраивать Корзину), Корзина так и остается невидимой, а страница сервиса получает соответствующее сообщение с ошибкой;
    * в случае, если сервер присылает какой-либо другой ответ, Корзина становится видимой и также отсылает сервису соответствующее сообщение - ошибку в случае провала запроса или пустой объект data в случае успеха;

4. **обработка на стороне сервиса**:  код на странице сервиса получает сообщение из фрейма и вызывает добавленные через метод `window.yb.addHandler()` обработчики, передавая в качестве параметра объект этого сообщения, и если запрос завершился удачно, метод `window.yb.isConnected()` начнет возвращать true;

5. **добавление позиции в корзину**:  с этого момента сервис может вызвать метод `window.yb.addItem()` с необходимыми параметрами: во фрейм будет передано соответствующее сообщение, которое будет далее транслировано серверу в **POST**-метод `cart/item/add`;
*при первом вызове `window.yb.addItem()` корзина получает service_id и service_order_id, запоминает их и далее возвращает сервису количество текущей позиции в заказе в соответствии с этими данными*

6. **обработка успешного запроса добавления позиции**: при успехе серверного запроса из фрейма на страницу сервиса будет послано сообщение с количеством текущей позиции, которое будет передано в качестве параметра добавленным посредством `window.yb.addHandler()` обработчикам;

<!-- 7. **обработка ошибок**: в случае, если какой-либо из запросов на сервер заканчивается ошибкой, фрейм начинает в течение одной минуты слать запросы списка позиций корзины (`/cart/item/list`), повторяющиеся с интервалом в 2 секунды, транслируя каждый пришедший ответ через postMessage на страницу сервиса, при этом метод window.yb.isConnected() будет возвращать false до тех пор, пока не придет валидный (без ошибки) ответ; -->

7. **перенаправление на страницу корзины**: при клике на фрейм происходит перенаправление окна сервиса на окно Корзины.

### Возможные коды ошибок Корзины:
Код ошибки  | Значение ошибки
------------|----------------------
0           | ошибка при обработке ответа от сервера
400         | Validation Error
403         | Not Authorized
404         | Not Found
500         | Internal Server Error
x           | ?csrf-ошибка?
