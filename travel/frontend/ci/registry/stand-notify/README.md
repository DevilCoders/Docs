## Notify about beta stand

#### Description

Пишет в тикет связанный с PR о собранном образе и ссылках на стенд(ы).
А также пишет в описание PR.

#### Environment variables

| Имя                 |                                                                          Описание                                                                          | Обязательность |
| ------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------: | -------------: |
| STARTREK_TICKET_ID  |                                                                Ключ тикета TRAVELFRONT-1234                                                                |             да |
| PULL_REQUEST_ID     |                                                                Номер пул реквеста в аркадии                                                                |    опционально |
| APP_VERSION         |                                                     Версия приложения, совпадает с тегом докер образа                                                      |             да |
| STAND_URL           | Ссылка на стенд, например https://pr-${context.launch_pull_request_info.pull_request.id}.unstable.pdf.common.yandex.net (либо несколько с переносом строк) |             да |
| CROWDTEST_STAND_URL |                                                    Ссылка на стенд через прокси для внешних сотрудников                                                    |    опционально |
| TRAVEL_CI_PATH      |                                                            Путь до папки с ci фронтенда портала                                                            |             да |
| STARTREK_TOKEN      |                                                                Секретный токен доступа в ST                                                                |    опционально |
| ARCANUM_TOKEN       |                                                             Секретный токен доступа к аркануму                                                             |             да |
