# Тесты на бэк календаря

### Первоначальная настройка
- Получите любую роль в сервисе в [ABC](https://abc.yandex-team.ru/services/testopithecus/)
- Устаналиваем arc, скачиваем аркадию и настраиваем automount https://wiki.yandex-team.ru/mobvteam/arc-macos/#ide
- Скачиваем WebStorm
- Открываем проект XMail в WebStorm. Он лежит по пути `mail/common/xmail`
- Устанавливаем последнюю ноду ```brew install node```
- Устанавливаем ярн ```brew install yarn```
- Устанавливаем зависимости - в корне xmail запускаем `yarn`

### Запускаем тесты
- Заменяем `tvmtool.conf` в репозитории на `tvmtool.conf` из секрета https://yav.yandex-team.ru/secret/sec-01ee7xdb2nb654sk1nvyw99ve5 
- Справа сверху выбираем и запускаем конфигурацию `Start Calendar TVM tool on port 2222`

#### Запускаем рандомный обход
- Справа сверху выбираем и запускаем конфигурацию `Run random walk on calendar backend` - запустится тест 
`Случайное блуждание.должно проверять синхронизацию, обходя известные баги` из `calendar.test.ts`
- Могут заинтересовать две константы:
    * `syncronizationDelaySec` - это промежуток времени после создания события, когда мы закрываем глаза на рассинхрон
    * `maxEvents` - на каком уровне будет болтаться число событий, которые участвуют в тесте
    * `maxBackendRetries` - число попыток на GET-запросы к нашему бэку
    * `allowEmptyEvents` - разрешить создавать события с нулевой длиной
    * `allowAttendeeDetach` - разрешить удалять участников событий
    * `stepsLimit` - количество шагов случайного блуждания

#### Запускаем фиксированные тесты
    
- Берем токен для TUS (Test User Service) https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9052de6e4cf142039a7ee44ac03e4614
- Сохраните его в `~/.tus/token`
```
mkdir -p ~/.tus ; chmod 700 ~/.tus ; echo 'TOKEN' > ~/.tus/token ; chmod 400 ~/.tus/token
```
- Пока что только один пользователь в тестинге подходит для тетсов `наш бэк vs exchange`. Его надо указать в `getDebugAccount` в `UserServiceEnsemble`
```
case AccountType2.YandexTeam:
        return new UserAccount('calendartestuser@yandex-team.ru', '', '1120000000004717')
``` 
(пароль не нужен)
- Справа сверху выбираем и запускаем конфигурацию `Run all tests on calendar backend` - запустится тест из `calendar.test.ts`
