### Нюансы сборки
- Таска из-за tvm работает только в бинарном режиме(https://docs.yandex-team.ru/sandbox/dev/binary-task)
- Дефолтные параметры в форме обновляются, только после коммита

### Сборка и отладка
Для отладки можно использовать
```bash
ya make -tAP && ya make
# команда вернёт ссылку на sandbox в котором
# дозаполнив форму можно таску запустить и проверить без коммитов
./DnsDutyNotificationNewAbcApi run --create-only
# команда загружает бинарь, который при создание таски
# надо заиспользовать как ресурс
./DnsDutyNotificationNewAbcApi upload
```

### Обновление
После прохождение всех тестов в ПР и мёрдже:
1. склонировать и запустить(ничего не меняя) SB таску DEPLOY_BINARY_TASK: https://sandbox.yandex-team.ru/task/1300911557/view
2. на вкладке Resources перейти в SANDBOX_TASKS_BINARY и нажать на флажок Important или проставить параметр ttl:inf
3. переходим в Scheduler task https://sandbox.yandex-team.ru/scheduler/711183/view и нажимаем редактировать
4. нужно раскрыть спойлер Advanced и в нём отредактировать поле Tasks resource вбив номер нового ресурса с SANDBOX_TASKS_BINARY, а старый удалить
5. нажать внизу кнопку Save

Enjoy
