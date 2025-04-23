# Тестовая/тренировочная звонящая проверка

## Что такое, зачем { #theory }

Juggler-проверка, которую можно зажигать когда удобно.  
Нужна, чтобы спокойно потренироваться останавливать эскалацию.  
Смотрит на наличие файла `/tmp/test-juggler-check-file` на ppcback-ах.


## Потренироваться принимать звонок

**1.** Убедиться, что проверка зеленая:  
<https://juggler.yandex-team.ru/check_details/?host=direct.backs&service=test-juggler-check&query=&last=1DAY>

**2.** Создать файл, на который завязана проверка:  
```
executer exec %direct_backs touch /tmp/test-juggler-check-file
```

**3.** Дождаться, что проверка покраснеет:  
<https://juggler.yandex-team.ru/check_details/?host=direct.backs&service=test-juggler-check&query=&last=1DAY>  
Это происходит за 1-2 минуты.

**4.** Дождаться звонка от мониторинга (должен произойти сразу, как покраснеет).  
Остановить эскалацию: нажать 4.

**5.** Убедиться, что эскалация остановилась (в списке должно быть пусто):  
<https://juggler.yandex-team.ru/escalations/?query=recipient%3Dlena-san%7Crecipient%3Drobot-direct-admin>

**6.** Удалить файл, на который завязана проверка:  
```
executer exec %direct_backs rm /tmp/test-juggler-check-file
```

**7.** Дождаться, что проверка позеленеет:  
<https://juggler.yandex-team.ru/check_details/?host=direct.backs&service=test-juggler-check&query=&last=1DAY>


## Что где { #moving-parts }

Тикет, в котором провеку делали:  
<https://st.yandex-team.ru/DIRECTADMIN-9186>

Конфиг monrun для ppcback:  
<https://a.yandex-team.ru/arc/trunk/arcadia/direct/packages/yandex-du-test-juggler-check/etc/monrun/test-juggler-check.conf>

Проверка, сконфигурирована вручную в интерфейсе Juggler:  
<https://juggler.yandex-team.ru/check_details/?host=direct.backs&service=test-juggler-check&query=&last=1DAY>

Правило нотификации, сконфигурировано вручную в интерфейсе Juggler:  
<https://juggler.yandex-team.ru/notification_rules/?query=rule_id=606c1727e9dc320314fa14cb>


