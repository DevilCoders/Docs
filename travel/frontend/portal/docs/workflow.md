# Workflow

## Работа над задачей

> Ниже представлен алгоритм, рекомендуемый для большинства задач.

1. Ознакомится с описанием, задать интересующие вопросы в трекере, проверить статусы готовности по смежным проектам.
2. Переводим статус задачи в состояние "В работе".
3. Создаем ветку от ветки trunk c названием: [task-id]-task-name или просто [task-id], примеры: TRAVELFRONT-1234, TRAVELFRONT-1234-remove-hotelname.
4. Названия коммитов (отражающие суть коммита) -- на ваше усмотрение.
5. После завершения работы над задачей создаем PR в trunk. Название берем из тикета, пример: "TRAVELFRONT-2341: Ошибка в выдаче на все дни". task-id нужен для попадания задачи в релизный тикет при его сборке. Арканум автоматически добавит человека на ревью.
6. Проверяем статусы прохождения тестов и линтеров.
7. Публикуем PR, статус задачи в состояние "Ревью" переходит автоматически в трекере.
8. После успешного прохождения ревью тикет автоматически переводится в статус "Можно тестировать". Если этого не произошло, то переводим тикет вручную.
9. Проверить, есть ли ответственный QA-инженер, по возможности описать примерную последовательность при тестировании.
10. QA-инженер должен перевести статус задачи в состояние "Тестируется" и провести тестирование функциональности, ветка с PR должна расскатится на специальный стенд на ферме.
11. При успешном прохождении тестирования перевести статус задачи в состояние "Протестировано", при наличии багов или переоткрыть или написать в комментарии, если правки небольшие.
12. Выполняем merge PR в trunk.
