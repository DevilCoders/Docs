## Состояния заказов

Этот документ описывает состояния, в которых может находиться заказ, а также
возможные внешние события, на которые он должен уметь реагировать.

Заказ может находиться в одном из состояний:

* `draft` - за заказом зарезервирован id.
* `pending` - идет процесс поиска исполнителя заказа.
* `assigned` - заказ назначен на исполнителя.
* `cancelled` - заказ отменен пользователем.
* `finished` - заказ помечен системой как находящийся в терминальном состоянии.
* `reordered` - пользователь прекратил поиск исполнителя на заказ и создал
                новый заказ с другими критериями поиска.

При проектировании матрицы переходов следует исходить из предположений, что

* из-за сетевых задержек запросы могут приходить в разном порядке, задваиваться.
* работа систем client, taxi и STQ ведется настолько небольшими интервалами,
  что полагаться на то, что с момента последнего запроса в системе ничего не
  изменилось, нельзя.

## Переходы

### /commit
Получив на руки номер черновика (вполне возможно, что после нескольких попыток
его создания), клиент подтверждает факт заказа. Если переданный заказ и правда
является черновиком, будут выполнены необратимые операции:

1. Списание тестового рубля (только для новых заказов, не для /reorder-ов).
2. Блокирование купона (только для новых заказов, не для /reorder-ов).

Отдельного внимания заслуживает процедура `check_card`.
Это STQ-процедура, поэтому результат ее вызова может стать известен
в любой момент.
Эта проблема решается сделующим образом.

1. В момент создания reorder-заказа, родительский заказ получает поле child_id,
   где записан id наследника.
2. Если процедура `check_card` видит, что она пытается обновить данные у заказа
   с непустым `child_id`, она обновляет заказ-наследник, а не исходный заказ.
3. Если же процедура `check_card` была завершена до того, как был сделан
   `reorder`, (или если пользователь имеет симпанию к нашему сервису),
   у заказа будет выставлено поле `check_card_is_finished`, и мы должны будем
   перенести данные, выставленные `check_card`-ом в новый документ.

### /reorder
В какой-то момент времени клиент решает изменить условия поиска.
Клиенту кажется, что в этот момент заказ находится в состоянии `pending`.

На сервере выполняется следующий набор инструкций:

1. Создается черновик заказа, запоминается его id.
2. Если заказ был в состоянии `pending`, то переводим заказ в состояние
   `reordered`, параллельно присваивая нужное значение полю `parent_id`
   (значение из черновика заказа). Если сразу после этого клиент решит
   обратиться к серверу и узнать о состоянии заказа, он уже увидит корректный
   `reordered` заказ. Более того, заказ с id `parent_id` так же уже будет
   в системе и его статус можно будет проверить.
   Как только мы убеились, что состояние заказа и правда было `pending`, мы
   инициируем поиск водителей на заказ. Так же инициируется рассылка
   `cancelrequest`-ов паркам.
3. Если состояние заказа было `assigned`, то мы должны в ответе вернуть просто
   id текущего заказа. Важно, чтобы проверка на состояние `assigned`
   осуществлялась после проверки на состояние `pending`. Потому что иначе обе
   проверки могут закончится неудачей.
4. `cancelled` заказ не может быть `reordered`. С точки зрения backend-а
    невозможно понять, что именно хотел сделать пользователь.
5. `finished` заказ не должен переходить в статус `reordered`, так как
   `finished` это терминальное состояние. И у нас нет возможности отследить
   задвоение заказа.
6. Если заказ находится в статсусе `reordered`, то скорее всего, это означает
   задваивание вызова, например, в результате сетевой ошибки при получении
   клиентом ответа от предыдущего вызова `/reorder`. Но лучше не пытаться
   решить эту проблему, а сказать клиенту, что что-то пошло не так.
