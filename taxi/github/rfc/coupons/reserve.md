### Описание работы ordercommit через сервис купонов

#### Проблема
До перехода на сервис, промокоды отключить было невозможно. Это значило, что, если не удалось проверить промокод - ordercommit отвечал 500 и не давал сделать заказ. 

С появлением сервиса, промокоды должны быть отключаемыми. Поэтому нужна отказоустойчивая схема на тему "Как обрабатывать ошибки".
Есть несколько моментов на которые стоит обратить внимание.
1. Что делать, если сервис отвечает 4xx?
2. Что делать, если сервис отвечает 5xx?
3. Что делать, если сервис таймаутит.

Если в первом случае запрос скорее всего не дошел до сервиса, то в остальных кейсах невозможно сказать был ли зарезервирован промокод или нет. Эти и другие случаи нужно уметь корректно обрабатывать

#### План решения
В качестве решения предлагается схема правок в трех местах


##### routestats
Когда в routestats отправляется купон, необходимо сделать полноценный чек через сервис купонов, и, в случае успешной проверки, записать информацию о купоне в оффер. Если сервис отвечает 400, 500 или таймаутом - в оффер ничего не пишем.
Таким образом, если в оффере окажется купон, то он гарантированно будет проверен, а поскольку время жизни оффера довольно мало, это позволяет сделать оптимизацию проверки в ordercommit


##### ordercommit
Сейчас купон через драфт записывается в ордер, далее ordercommit забирает купон из драфта и проводит reserve.
Предлагается также читать купон из оффера. При чтении купона из оффера можно сделать оптимизацию проверки: т.к. мы знаем, что купон прошел проверку в routestats, можно сделать короткую проверку на лимиты. Это значительно снизит вероятность сбоя, т.к не нужно будет ходить в биллинг и userstats.
- Если купона в оффере не будет, то в ордере делаем полную проверку.
- Если купон в оффере не соответствует купону в ордере - бросаем PRICE_CHANGED.
- Если купон есть в оффере, а в ордере нет - бросаем PRICE_CHANGED.

Таким, образом получаются следующие варианты развития событий:
Ничего не делать:
- Нет оффера, нет купона из драфта
- Есть оффер без купона, нет купона из драфта
- Есть оффер с купоном, нет купона из драфта

Нужна полноценная проверка и reserve купона:
- Нет оффера, есть купон из драфта
- Есть оффер без купона, есть купон из драфта

Нужна урезанная проверка на лимиты и reserve купона:
- Есть оффер с купоном, есть купон из драфта


##### couponreserve
В сервисе купонов необходимо поддержать возможность короткой проверки через параметр check_type.
Также запросы резерва в монгу необходимо сделать идемпотентными, чтобы потенциальные ретраи не добавили лишнюю запись.


##### Обработка ошибок
Необходимо обрабатывать следующие ошибки:
- 4xx - Клиентская ошибка. 
ordercommit должен вернуть 500.

- 429 - Либо отключен сервис, либо слишком много запросов.
В этом случае нужно посмотреть был ли купон в оффере. Если да, то надо вернуть PRICE_CHANGED
Если купона в оффере не было - продолжаем коммит без купона.

- 5xx, timeout - Запрос не дошел до сервиса, сетевая ошибка.
Неизвестно был ли осуществлен reserve, поэтому надо произвести отмену резерва.
Также нужно посмотреть был ли купон в оффере. Если да, то надо вернуть PRICE_CHANGED
Если купона в оффере не было - продолжаем коммит без купона.
