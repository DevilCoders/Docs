### Что делает сервис
**reaper** - удаляет или обновляет подписки залогинового пользователя по событиям от Паспорта: обработка разлогина пользователя, реакция на смену пароля.

### Импакт на пользователей от отключения сервиса
Пользователь будет продолжать получать пуши после разлогина/смены пароля.

### Импакт остановки тачки/ДЦ
Балансер должен перенаправить нагрузку на другие тачки/ДЦ, нагрузка на них возрастет пропорционально.

### Особенности деплоя
Нет

### Критичные метрики
#### TODO: https://st.yandex-team.ru/MAILPG-3387

### Куда ходит
#### xivaconf
Периодически, раз в несколько минут, получает актуальный список паспортных сервисов.

#### xivahub
Не более одного раза на каждый запрос получает список подписок пользователя на сервис. В случае необходимости обращается для выполнения процедуры отписки и для отправки специальных уведомлений об отписке.
