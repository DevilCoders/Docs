# Что делает скрипт auto_switcher
Скрипт позволяет автоматически переключать квики на живой кластер.
В случае, если возможны оба варианта, приоритет отдается hahn.yt.yandex.net

# Вход
На вход подается путь к квикам, который по дефолту DEFAULT_QUICK_PATH = '//home/images/quick/rt_robot'

# Почему переключения не происходят часто?
Потому что переключения определяются исключительно 4-мя переменными в коде, описывающими
запланированные и экстренные работы на каждом из кластеров. Поскольку их значения меняются редко - редко и меняется
выполняемый if-блок.
