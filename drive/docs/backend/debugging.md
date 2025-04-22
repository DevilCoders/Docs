# Отладка бекенда

## GDB
Не стоит бояться подключаться с помощью gdb к процессу, в том числе, и в prodution-контейнерах. Запускать нужно версию со вкусом Яндекса:
```
ya tool gdb
```

Полезные команды:
```
thread apply all bt # вывести stacktrace'ы по всем потокам
```

## Логгирование
Есть несколько способов записывать отладочную информацию в коде:
- Global log: ```DEBUG_LOG, ERROR_LOG``` и т.д. Записывает произвольную (неструктурированную) информацию в лог **current-backend-global-log**, местный аналог ```std::cerr```. Запись происходит синхронно, лог ротируется каждые несколько часов
- Events log: ```NDrive::TEventLog::Log(...)```. Записывает Json сообщения в правильном формате в лог **current-backend-events-log**, который потом доставляется в YT для хранения в течение 25 лет. Запись происходит асинхронно (отдельным потоком)
- Thread event log: ```NThreading::GetEventLogger()->AddEvent(...), NThreading::BuildEventGuard("SectionName")```, также доступен напрямую в ручках в ```TJsonReport::TGuard::AddEvent```. Записывает произвольные Json в per-thread лог исполнения ручек, который либо discard'ится, либо записывается в ```event=EventLog``` в **current-backend-events-log**, либо выводится в ответе ручки при указании cgi-параметра ```&dump=eventlog```

Когда что использовать:
- Если это старт бекенда или фоновый процесс – **Global log**
- Если это отладочная информация о процессе выполнения ручки – **Thread event log**
- Если это информация, которую нужно сохранить на вечно в логи – **Events log**

## Задание запросов
Получаем OAuth токены на https://wiki.yandex-team.ru/Yandex.drive/carsharing/Разработка/devops-common/#poluchenieoauth-tokenov
Далее мы пользуемся curl'ом:
```
curl --request GET \
  --url 'https://stable.carsharing.yandex.net/user_app/sessions/current?dump=eventlog' \
  --header 'Accept-Language: en' \
  --header 'Authorization: OAuth YOUR_OAUTH_TOKEN' \
  --header 'DeviceID: YOUR_DEVICE_ID'
```
