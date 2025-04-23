# chassis - сборник инфраструктурных демонов и интерфейсов

### Ассоциация
Тележка, на которую можно навешать кучку функциональности

### Возможности (в процессе)
- шедулер (hourglass как в jobs, сейчас поддерживаются нешардированные/без параметров задачи)
- json-api
- internal-tools

### Локальный запуск
Запустить джобы можно из класса ChassisDebugApp.kt.

### Доступ к Стартреку
Для доступа к Стартреку нужно запустить `./bin/get_oauth_token.sh` из директории `${ARCADIA_ROOT}/direct`

Ссылка на исходник скрипта [get_oauth_token.sh](https://a.yandex-team.ru/arc/trunk/arcadia/direct/bin/get_oauth_token.sh)

Альтернативный вариант: [получить OAUTH-токен по этой ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b),
и записать результат в файл `~/.direct-tokens/local_user_oauth_token`
```(shell)
rm ~/.direct-tokens/local_user_oauth_token
echo "AQAD##################" > ~/.direct-tokens/local_user_oauth_token
```

### maintenance-helpers
Переехал в состав шасси. Для некоторых задач продолжает использовать собственные (от robot-direct-sustain) секреты.
По всем вопросам — обращайтесь к ppalex@.