Директория для хранения регулярных YQL-запросов команды **аналитики доставки**

Инструкция по добавлению запроса:

1. Создать новый файл и скопировать запрос из YQL-интерфейса, в названии указать название результирующей таблички + расширение .yql
2. Для запуска запроса необходимо создать кубик в Нирване по примеру: https://nirvana.yandex-team.ru/flow/15bde36f-002b-46b0-8e7f-87b3a09c6ade/ab8c66e5-2c4a-44d2-8bc4-ab5c610ffa8a/graph
    - Нужно будет единоразово получить токен Аркадии и положить его в секретницу: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5c407aafc5c242948b532842a9a07da6
    - Далее к графу можно прикруть реакцию и настроить регулярный расчет
    - Чтобы реакция выплевывала артефакт, нужно заполнить графу "Parametrs" -> "On sucsess" в настройках рекации (пример: https://reactor.yandex-team.ru/browse?selected=10269726)
3. Тык кнопочку "Commit" -> комментарий, что поменяли -> "Send to review"
4. Во вкладке "Pull Requests" необходимо сделать review и подтвердить мердж тыкнув "ship" / дождаться подтверждений от ревьюеров
    - Правила review задаются файликом a.yaml, применяются из первого файлика найденного по мере спусканию к корню
5. Дождать завершения мерджа
6. Profit!!!

Чтобы получить полный доступ (удаление файлов + добавление папок) необходимо установить arc на локальную машину по инструкции: 	
- https://docs.yandex-team.ru/devtools/intro/quick-start-guide
