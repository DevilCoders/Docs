### Как получить тексты ответов?

1. Нужно в /etc/hosts прописать:
    ```
    127.0.0.1 greed-ts1f.yandex.ru
    ```
2. Открыть туннель:
    ```
    ssh -L 8018:greed-ts1f.yandex.ru:8018 gravicapa01ht.market
    ```
3. Запустить wiremock standalone:
    ```(bash)
    java -jar wiremock-standalone-2.6.0.jar \
    	--verbose \
    	--proxy-all="http://greed-ts1f.yandex.ru:8018" \
    	--record-mappings \
    	--port 14888 
    ```
4. Дергать нужные ручки.
