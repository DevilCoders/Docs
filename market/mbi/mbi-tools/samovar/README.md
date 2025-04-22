# Инструмент для скачивания фидов из самоварных бакетов в mds

Для работы скрипта нужен Python и библиотека requests.

Установить библиотеку requests можно с помощью команды `pip install requests`.

Запуск программы производится с помощью команды `python3 samovarFeedDownload.py -k '<MDS_KEY>' -o <OUTPUT_FILENAME>`. 

`<MDS_KEY>` - самоварные mds ключи в формате `1994427/b3bSroXrp7VkMP51em6FufIJCfe98Mkt|1781458/NBQrFQdLMUXK70sOqtSPA0abHeXQKu0g|` 
в кавычках, тк в bash'e `|` - это спецсимвол.

`<OUTPUT_FILENAME>` - имя выходного файла для скачанного фида.

