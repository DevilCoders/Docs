# timetarget - библиотека для работы с настройками временного таргетинга

### Формат хранения настроек
Формат:
```
( [1-9] ([A-X][b-jl-u]?){1,24} ){1,9}
   ^      ^    ^
   |      |    |
  (1)    (2)  (3)
```
Может быть до 9 групп, состоящих из:
1) `[1-9]`: id дня. 1-7 - дни недели, 8 - праздники, 9 - рабочие выходные
2) `[A-X]`: час. A - 00, B - 01, ..., X - 23
3) `[b-jl-u]`: коэффициент. `k` не используется, так как равно 100%. `a` равно 0% и тоже не используется.
Один шаг равен 10%. Возможный диапазон 0%-200%.

Примеры:
1JKLMNOPQ2JKLMNOPQ3JKLMNOPQ4JKLMNOPQ5JKLMNOPQ67 - показывать по будням с 09:00 до 17:00
1AcBcCcDcEFGHIJKLMNbOPQRSTUVcWcXc2AcBcCcDcEFGHIJKLMNbOPQRSTUVcWcXc3AcBcCcDcEFGHIJKLMNbOPQRSTUVcWcXc4AcBcCcDcEFGHIJKLMNbOPQRSTUVcWcXc5AcBcCcDcEFGHIJKLMNbOPQRSTUVcWcXc6AcBcCcDcEFGHIJKLMNbOPQRSTUVcWcXc7AcBcCcDcEFGHIJKLMNbOPQRSTUVcWcXc9 - выглядит так https://jing.yandex-team.ru/files/mspirit/timeTarget.jpg

### Хранение в БД
Настройки временного таргетинга определяются для кампании. Хранятся в `campaigns.timeTarget` и `campaigns.timezone_id`.

Перечень праздников и рабочих выходных (aka "Производственный календарь") хранится в таблице
[`ppcdict.great_holidays`](https://direct-dev.yandex-team.ru/db/ppcdict/tables/great_holidays.html).
