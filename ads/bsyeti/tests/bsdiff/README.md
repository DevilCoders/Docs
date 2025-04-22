Обновление тестовых данных

Использование: generate_test_data test_samples_count> <courgette_bsdiff_binary_path>

Потребуется собрать contrib/tools/courgette_bsdiff и подать путь к нему на вход скрипту.
Скрипт генерирует test_samples_count пар (база и декодированный) произвольных двоичных файлов, применяет к ним bsdiff для 
получения патча и складывает базу с патчем в bsdiff_test_data.tgz
После генерации тестовых данных bsdiff_test_data.tgz следует поместить в sandbox: ya upload --ttl=inf --do-not-remove bsdiff_test_data.tgz
Полученным идентификатором обновить параметры FROM_SANDBOX и DATA внутри ya.make теста
