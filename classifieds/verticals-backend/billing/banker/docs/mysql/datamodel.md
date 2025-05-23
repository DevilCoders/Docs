Описание таблиц банкира
==================================================================

Таблица account
------------------------------------------------------------------

Таблица содержит данные зарегистрированных пользователей.

#### id  
> Автоинкрементый интовый айдишник, используемый для внутренних связей. 

#### account_id
> Внешний айди пользователя в банкире (в случае авто.ру еще и айдишник кошелька).

#### user
> Айдишник пользователя авто.ру/недвижки.

#### properties и properties_string
> Дополнительные сведения о пользователе. Например, телефон или почта.
> Первый столбец хранит сериализованное представление соответствующей протомодели 
> Account.Properties в aschema-registry/proto/vertis/banker/api_model.proto
> Второй же столбец предназначен лишь для удобства пользователя бд.
> В нем содержится та же самая информация, но в человекочитаемом виде.

#### payload
> TODO

#### epoch 
> Дата последнего изменения строчки в таблице. 
> Аналогичное поле присутствует и в других таблицах банкира.


Таблица lock_account
------------------------------------------------------------------

Очень интересное решение. 

Каждый платеж в банкире проходит длинный путь от поступления в качестве 
запроса до подтверждения и последующего уведомления пользователя.
Мы не должны давать клиенту возможность выполнить второй платеж до подтверждения 
первого, так как при принятии запроса на платеж в обработку мы должны быть уверены, 
что на счету пользователя хватает средств для проведения операции, иначе бы 
у нас в системе при параллельной обработке двух платежей возник бы race condition, 
который мы разрешаем добавлением своеобразного мьютекса -- данной таблицы.

TODO Подробности, каким конкретно образом лочится пользователь не знаю.


Таблица yandexkassa_v3_payment_request
------------------------------------------------------------------

Одна из первых таблиц, куда попадает запрос на платеж.
Когда клиент хочет совершить оплату, он отправляет нам запрос в ручку платежей.
Полученный данные преобразуются, записываются в данную таблицу и остаются там, 
пока пользователь не произведет оплату услуги через платежную систему. 

#### pr_id (payment_request_id)
> Айдишник запроса платежа, задаваемый банкиром, для внутреннего использования.

#### account_id
> Позволяет идентифицировать пользователя, совершающего платеж. Связан с **account.id**

#### amount
> Сумма платежа. Будет положительным, если клиент пополняет кошелек или возвращает средства.
> Если платеж -- списание, то amount < 0.

#### method_id
> Метод оплаты, которым хочется совершить платеж. 
> Связан с таблицей **yandexkassa_v3_payment_method**, о которой речь пойдет чуть позже.

#### payload и payload_string
> Полезная нагрузка, которую нам передал клиент. Она никак не влияет на работу сервиса. 
> Просто, иногда клиентам удобно передавать нам данные на хранение на протяжении всего 
> цикла обработки, чтобы в конце вместе с результатом получить их обратно.
> По аналогии с **account.properties** храним тут байты протомодели, а в соседней колонке 
> читаемое человеком представление. 

#### options и options_string
> TODO

#### receipt и receipt_string
> TODO

#### form и form_string
> TODO Протомоделька формы оплаты.....

#### context и context_string
> TODO Пополнение или покупка

#### epoch
> Дата последнего изменения строчки в таблице

#### refund_for
> Если данный платеж является возвратом, то будет иметь значение, иначе null.
> Айдишник платежа (TODO какой, не увидел связи), возврат которого мы оформляем.


Таблица yandexkassa_v3_payment_external_request
------------------------------------------------------------------
При записи в таблицу yandexkassa_v3_payment_request, часть данных запроса попадает
в эту таблицу. Сюда записывается целиком весь запрос в формате json (поле **source**).
#### p_id
> айдишник платежа в юкассе. TODO ?заполнится до подтверждения или после?

#### external_id
> TODO

#### status
> TODO

#### epoch
> Дата последнего изменения строчки в таблице.
> Аналогичное поле присутствует и в других таблицах банкира.


Таблица yandexkassa_v3_payment_method
------------------------------------------------------------------
Информация по методам оплаты, доступным через юкасссу.

#### method_id
> Название метода оплаты. Например: qiwi, sberbank, tinkoff_bank

#### effective_since
> Дата, начиная с которой данный метод оплаты доступен для использования в платежной системе.

#### rank
> TODO Мы по нему ищем. Но кто он?.. 

#### downtime_until
> Дата до которой соответствующий метод оплаты не доступен.

#### epoch
> Дата последнего изменения строчки в таблице.
> Аналогичное поле присутствует и в других таблицах банкира. 


Таблица yandexkassa_v3_payment
------------------------------------------------------------------
В эту таблицу попадает уже подтвержденная платежной системой операция.

#### p_id
> Идентификатор платежа. Ссылается на айдишник соответствующего запроса 
> (p_id -> {...}_payment_request.pr_id).

#### raw
> TODO

#### invoice_id
> TODO Тот же payment_external_request.p_id, как будто, только на него нет ссылок.

#### payment_status
> Created или Processed

#### epoch
> Дата последнего изменения строчки в таблице.
> Аналогичное поле присутствует и в других таблицах банкира.
