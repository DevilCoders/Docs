# Статусная модель

В данном разделе рассматриваются:

* стадии, которые проходит заявка на доставку в процессе обработки;

* методы АPI, доступные на конкретной стадии заявки и изменяющие состояние заявки.

## Этапы создания и исполнения заказа {#process}

* На этапе [формирования заказа](#create) новая заявка проходит проверку и оценку, производится поиск исполнителя заказа.

* Если заказ сформирован успешно, водитель приезжает к отправителю и [получает товар](#pickup) для доставки.

* После успешного получения товара исполнитель [доставляет заказ](#delivery) по указанным адресам.

* Если какой-то из товаров не удалось доставить, производится [возврат товара](#return) на точку возврата.

На всех этапах создания и обработки заказа вам доступно [получение информации](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) о заявке. [Журнал изменений заказа](https://yandex.ru/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsJournal.html) позволяет отслеживать историю заявки.

![Схема формирования заказа1](https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/api/files/status-model-1-ru.png)

![Схема формирования заказа2](https://yastatic.net/s3/doc-binary/src/dev/logistics/ru/api/files/status-model-2-ru.png)

<style>
    .doc-c-number-in-circle { width: 25px;
        height: 25px;
        line-height: 25px;
        -moz-border-radius: 50%;
        border-radius: 50%;
        background-color: #333333;
        color: #FFFFFF;
        text-align: center;
        display: inline-block; }
</style> 

## Формирование заказа {#create}

<span class="number-in-circle">1</span> Запрос [Создание заявки с мультиточками](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsCreate.html) инициирует процесс формирования заказа.

<span class="number-in-circle">2</span> После создания заявки запустится процедура оценки заявки. Чтобы узнать результат оценки, выполните запрос [Получение информации по заявкам с учетом мультиточек](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html).

<span class="number-in-circle">3</span> В случае успешной оценки заявка переходит в состояние ожидания подтверждения. Запрос на [получение информации о заявке](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) вернет стоимость заказа для клиента. При необходимости отредактируйте заявку с помощью метода [Редактирование заявки с мультиточками](https://yandex.ru/dev/logistics/api/ref/claim-edit/IntegrationV2ClaimsEdit.html). После редактирования заявка автоматически отправляется на оценку. Чтобы подтвердить заявку, отправьте запрос [Подтверждение заявки](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsAccept.html) в течение 10 минут после присвоения заявке статуса `ready_for_approval`.

<span class="number-in-circle">4</span> Не удалось оценить заявку. Запрос на [получение информации о заявке](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) в поле `error_messages` вернет причины, по которым заявка не может быть исполнена. Заявку можно отправить на повторную оценку после [редактирования](https://yandex.ru/dev/logistics/api/ref/claim-edit/IntegrationV2ClaimsEdit.html).

<span class="number-in-circle">5</span> После подтверждения заявки запускается процесс поиска исполнителя.

<span class="number-in-circle">6</span> Если вы подтвердили заявку после истечения 10 минут с момента присвоения заявке статуса `ready_for_approval`, заявка перейдет в состояние ошибки. В таком случае создайте новую заявку.

<span class="number-in-circle">7</span> Производится поиск исполнителя заказа в соответствии с указанными в заявке требованиями.

<span class="number-in-circle">8</span> Подобран исполнитель для вашей заявки.
С этого момента и до завершения заказа вы можете запрашивать следующую информацию:

* Данные о водителе и транспортном средстве — метод [Получение информации по заявкам с учетом мультиточек](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html), поле `performer_info` ответа.

* Номер телефона водителя — метод [Получение номера телефона для звонка водителю](https://yandex.ru/dev/logistics/api/ref/performer-info/IntegrationV1DriverVoiceForwarding.html). Если водитель будет заменен по какой-либо причине, перезапросите номер телефона.

* Координаты текущего местоположения исполнителя — метод [Получение позиции исполнителя заявки](https://yandex.ru/dev/logistics/api/ref/performer-info/IntegrationV1ClaimsPerformerPosition.html).

<span class="number-in-circle">9</span> Исполнитель не был найден или отменил заказ. Попробуйте создать новую заявку.

{% note info "Примечание." %}

На всех стадиях формирования заказа до начала его исполнения вам доступна возможность бесплатной отмены заявки. Чтобы отменить заявку:

1. Убедитесь, что вам доступна бесплатная отмена заявки — метод [Получение информации по заявкам с учетом мультиточек](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html), поле `available_cancel_state` ответа.

2. Отмените заявку — метод [Отмена заявки](https://yandex.ru/dev/logistics/api/ref/cancel-and-skip-points/IntegrationV2ClaimsCancel.html).

{% endnote %}

## Получение товара водителем {#pickup}

<span class="number-in-circle">10</span> Водитель приехал на точку А, чтобы забрать заказ. После того как водитель сообщит системе, что он забрал заказ, автоматически сгенерируется код подтверждения. Отправитель может получить этот код через личный кабинет, SMS или с помощью метода API [Получение кода подтверждения](https://yandex.ru/dev/logistics/api/ref/confirmation-code-and-acts/IntegrationV2ClaimsConfirmationCode.html).

<span class="number-in-circle">11</span> Водитель ждет, когда отправитель передаст ему код подтверждения.

<span class="number-in-circle">12</span> Водитель ввел код подтверждения в систему. Получение водителем заказа теперь подтверждено. Запрос [Получение информации по заявкам с учетом мультиточек](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) в поле `visit_status` вернет информацию о посещении точки.

На стадиях 10 и 11, после того как водитель прибыл за заказом, но еще не получил его, существует возможность платной отмены заказа с помощью метода [Отмена заявки](https://yandex.ru/dev/logistics/api/ref/cancel-and-skip-points/IntegrationV2ClaimsCancel.html).
На стадии 12 отменить заказ можно только через службу поддержки. В этом случае водителю придется возвращать товар.

## Доставка товара {#delivery}

<span class="number-in-circle">13</span> Водитель приехал на точку Б, чтобы доставить груз получателю. После того как водитель сообщит системе, что он готов завершить заказ, автоматически генерируется код подтверждения и направляется получателю по SMS.

<span class="number-in-circle">14</span> Водитель ждет, когда получатель передаст ему код подтверждения.

<span class="number-in-circle">15</span> Водитель ввел код подтверждения в систему. Доставка получателю теперь подтверждена.
    Если доставлены еще не все грузы, водитель отправляется к следующему получателю.

<span class="number-in-circle">16</span> Все грузы доставлены получателям.

<span class="number-in-circle">17</span> Если хотя бы один груз по какой-либо причине невозможно передать получателю, по окончании доставки происходит возврат груза. По умолчанию точка возврата совпадает с точкой А, при необходимости можно указать другой адрес возврата.

На стадиях 13 и 14, до передачи груза курьеру, существует возможность отменить заказ через службу поддержки. В этом случае водителю придется возвращать груз.

## Возврат товара {#return}

<span class="number-in-circle">18</span> Водитель приехал на точку возврата. После того как водитель сообщит системе, что он вернул заказ, автоматически сгенерируется код подтверждения. Отправитель может получить этот код через личный кабинет, SMS или с помощью метода API [Получение кода подтверждения](https://yandex.ru/dev/logistics/api/ref/confirmation-code-and-acts/IntegrationV2ClaimsConfirmationCode.html).

<span class="number-in-circle">19</span> Водитель ждет передачи ему кода подтверждения.

<span class="number-in-circle">20</span> Водитель ввел код подтверждения в систему. Возврат товара теперь подтвержден.
