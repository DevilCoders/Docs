# Генерация патронов
 
Патроны генерируются sandbox задачей `MAPS_AMMO_GEN_FROM_YT` из yaml конфиг-файла.
Задача `MAPS_AMMO_GEN_FROM_YT` запускает `GENERATE_AMMO_FROM_YT` (удобно использовать, чтобы проверять корректность YQL запросов без коммита конфиг-файла).
Полученный файл с патронами загружается по пути `https://proxy.sandbox.yandex-team.ru/last/AMMO_FILE?attrs=%7B%22ammo_label%22%3A%22LABEL%22%7D`
где `LABEL` - это корневой ключ словаря из конфигурационного файла (например, `maps_road_events_renderer_regression_ammo`)
