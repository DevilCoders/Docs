## Длинная задача перевода результата валидации mpro в Задания НЯК

Считывает результаты проверок валидации mpro из базы validation.task_message

Записывает их в виде гипотез об ошибках в НЯК в базу social.feedback_task

### алгоритм:

1. Получает от пользователя запрос задач, которые пользователь хочет выгрузить. Параметры запроса:
- validationTaskId - обязательное, номер валидации
- severity - необязательное, серьезность ошибки
- checkId - необязательное, название проверки валидации
- description - необязательное, описание найденной ошибки
- importantRegion -  необязательное, важность региона

2. Получает из базы validation.task_message таски валидации, соответствующие запросу.

3. По истории запросов из service.validation_feedback_converter_task получает запросы, которые уже выполнялись с таким же validation_task_id, выгружает из базы validation.task_message список тасков валидации, которые уже выполнились.

4. Проверяет, что новые таски не лежат в списке уже выполненных тасков валидации. Не выполняет таск, если он уже выполнен. Так в НЯК не создаются одинаковые задачи, если у них один validation_task_id. Но тут остается проблема, что разные валидации с разными validation_task_id могут создать таски с одинаковым содержанием.

5. Пытается преобразовать таски валидации в таски фидбека.
- смотрит на поле the_geom: если там написана точка или многоугольник, преобразует его в точку и пишет в поле position. если пусто, таск не может преобразоваться
- смотрит на поле description: проверяет, что такой description воркер может обработать, создет description_i18n. Сейчас для больштнства описаний перевод берется такой же, как в mpro. Если проверка валидации заключалась в проверке уникальности адресов и нашлись два объекта с одним адресом, то для нового описания берется описание из mpro и добавляются две ссылки на объекты с одинаковыми именами
- по полю check_id получает тип задачи фидбека

6. Пишет результат в social.feedback_task