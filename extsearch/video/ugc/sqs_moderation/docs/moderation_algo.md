### Статусы

|  State           | Модерация завершена | Доступно для просмотра | Подсветить поле  | Текст | Комментарий |
|------------------|---------------------|------------------------|------------------|-------|-------------------|
| success          |    +                |   +                    |                  | опубликовано | одобрено 
| fail             |    +                |                        |         +        | забанено     | запрещено
| error            |    +                |   +                    |                  | ошибка       | ошибка вызова проверок, условно одобрено
| partial_success  |                     |                        |                  | в процессе   | прошла часть проверок, они одобрили. Все ещё может быть запрещено
| partial_fail     |                     |                        |                  | в процессе   | прошла часть проверок, они запретили. Может быть разрешено при получении финальных статусов
| old_success      |                     |   +                    |                  | опубликовано | перемодерируется после успеха
| old_fail         |                     |                        |                  | в процессе   | перемодерируется после провала


### Общий статус
* `None` - если все `None` (`None, None, None`)
* `error` - если все `error` (`error, error, error`)
* `fail` - если хоть один `fail` (`success, fail, None`)
* `old_fail` - елси оть один `old_fail` (`old_fail, ols_success, success`)
* `old_success` - елси оть один `old_success` (`None, old_success, success`)
* `partial_fail` - если хоть один `partial_fail` (`partial_fail, success, success`)
* `partial_success` - если хоть один `partial_success` или `None` (`None, success, success`)
* `success` - если все success или `error` (`success, error, success`)

Если по какому-то полю текущее значние не соответствует сохраненyому в info,
при расчете общего статуса модерации его статус считается как имеющий префикс `old_`

### Поля

* `tags` - тэги
* `title` - заголовок
* `description` - описание виде 
* `thumbnail` - preview

### При редактировании необходимо 

Поменять на old_fail если были изменены все поля со статусом fail
Поменять на old_success если было изименено любое поле со статусом success.


### При получения события об изменении поля необходимо
1. Проверить, что модерация не начата для данного значения
2. Запустить модерацию 
3. Сохранить для какого значения она запущена

### При получении результата модерации нужно
1. Проверить что актуальное значение поля совпадает с тем, которое модерировали
2. Пересчитать общий результат
3. Сохранить результат по полю и общий
