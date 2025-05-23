Как мы выбираем номер для редиректа
------------------------------------

Сейчас есть две фазы получения редиректа в getOrCreate 

#### Получение и проверка существующих редиректов

Смотрим, какие редиректы уже есть для target + objectId + tag. 
Из существующих редиректов исключаем те, которые не подходят по дополнительным параметрам (явно заданный geoId или тип телефона).
Оставшиеся размечаем на группы: относится к unhealthy или suspended оператору, является временным.
Редиректы сортируем по дате создания, от новых к старым. 


Выставляем предпочтения:
1. Просто подходящий редирект
2. С жалобой
3. suspended (выводим номера из оператора)
4. unhealthy (оператор сейчас считается сломанным, создаем временные редиректы на других операторах)

(1) возвращаем клиенту, для остальных случаев пробуем создать более подходящий редирект. 
Если создать не получилось, то отдаем, что есть. То есть предпочитаем отдать некачественный редирект, чем ничего 

#### Создание нового редиректа

По запросу (и наличию в нем явных указаний на гео и оператора и тип телефона) мы собираем возможные наборы (оператор, регион, тип телефона).

Алгоритм следующий:
1. Если явно указан оператор в запросе, то оставляем только его в кандидатах (используется скорее для дебага)
2. Убираем варианты, где нет свободных телефонов
3. Убираем временно недоступных операторов, если есть другие операторы. 
**todo** какая-то странная стратегия. Не правильней ли сортировать?
4. Убираем unhealthy, если уже есть unhealthy редирект
5. Убираем suspended, если уже есть suspended редирект
6. Предпочитаем операторов с бОльшим процентом свободных номеров.
Стараемся не использовать оператора, если у него осталось меньше 10% свободных номеров (в регионе, того же типа телефона)
7. Предпочитаем выдавать номер того же оператора, что и target номер. В надежде, что оператор сам с собой работает лучше
8. Предпочитаем не suspended операторов
9. Предпочитаем healthy операторов
10. Убираем операторов, на которые уже было больше одной жалобы с данным target-номером

Правила применяются именно в этом порядке. То есть сначала убираем, потом фактически сортируем по предпочтениям.
