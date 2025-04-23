# hub
Сервис для автоматизации рутинных задач в процессе разработки. 

[Документация.](https://wiki.yandex-team.ru/vertis-admin/hub/)
[Сборка в teamcity.](https://t.vertis.yandex-team.ru/project.html?projectId=VertisAdmin_Hub&tab=projectOverview) 
[Логи в новых логах.](https://admin.vertis.yandex-team.ru/logs?layer=prod&period=2h&limit=100&service=hub)

## Разработка 

### Локальный запуск 
Пока сервис не умеет переменные окружения, он работает с локальным файлов datasources. 
Для локального запуска нужны переменные из [датасурсов](https://github.com/YandexClassifieds/datasources/blob/master/roles/vertis-datasources/templates/testing.properties.j2#L3617). 
В тестах используется env GITHUB_API_TOKEN, позже он будет передаваться как часть конфигурации. 

Чтобы локально проверять работу хуков gh, можно воспользоваться https://ngrok.com.

Тесты запускаются через make test. 
