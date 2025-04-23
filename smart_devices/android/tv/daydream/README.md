# Day Dream
### The screen saver for android TV

Не на всех теликах получилось настроить **DayDream** через системные настройки.
В этом случае подключаем так:
```bash
# Включаем screen saver
adb shell settings put secure screensaver_activate_on_sleep 1
# Записываем нужный компонет в качестве дефолтного screen saver-а
adb shell settings put secure screensaver_default_component packageName/serviceName
# Записываем нужный компонет в качестве текущего screen saver-а
adb shell settings put secure screensaver_components packageName/serviceName
# Интервал ожидания (5 мин)
adb shell settings put secure sleep_timeout 300000 
```