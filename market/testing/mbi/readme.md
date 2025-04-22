==Как быстро запустить тесты


...как самому запускать тесты на релиз на мт10:

1. Установить pip (пакетный менеджер для питона): https://pip.pypa.io/en/stable/installing/

2. Пипом установить две либы:
$ [sudo] pip install lxml
$ [sudo] pip install requests


Скачать тесты:
svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/testing/mbi

cd mbi

$ ./test_moderation.py

