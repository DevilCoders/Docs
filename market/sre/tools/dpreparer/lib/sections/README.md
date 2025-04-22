# Инструкция по добавлению новой секции

1. Создаем в данном каталоге файл с классом, унаследованным от Section (lib.models.section).
1. Имплементируем метод execute().
1. Добавляем секцию в section_names класса Block (lib.models.block).
1. Добавляем в схему schemes.py и примеры examples.py (lib.schemes).
1. Пишем тесты.
