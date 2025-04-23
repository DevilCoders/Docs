Тестируем через ya make -t

Собранный тест можно запустить заново как бинарник. Запуск собранного бинарника может потребовать дополнительных
переменных окружения.

```bash
DJANGO_SETTINGS_MODULE=travel.avia.ticket_daemon_api.smalltests.tests_settings
# Используется для подгрузки тестовых django настроек

Y_PYTHON_SOURCE_ROOT=<your arcadia root>
# Позволяет запускать новые исходники не пересобирая тест
```
