Обновление тестовых данных

Использование: generate_test_data <test_samples_count> <xdelta3_tool_binary_path>

Потребуется собрать ads/bsyeti/tests/xdelta3/simple_tool и подать путь к нему на вход скрипту.
Скрипт генерирует test_samples_count пар (база и декодированный) произвольных двоичных файлов, применяет к ним xdelta3 для 
получения патча и складывает базу с патчем в xdelta3_test_data.tgz
После генерации тестовых данных xdelta3_test_data.tgz следует поместить в sandbox: ya upload --ttl=inf --do-not-remove xdelta3_test_data.tgz
Полученным идентификатором обновить параметры FROM_SANDBOX и DATA внутри ya.make теста
