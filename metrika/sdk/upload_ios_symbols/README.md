# Скачивание и выгрузка системных iOS символов в AppMetrica

## developer_apple_helper

Предоставляет методы для работы с сайтом https://developer.apple.com.
Умеет логиниться на сайте, парсить https://developer.apple.com/download/ и скачивать ipsw.

`login.rb` написан на ruby, т.к. для работы с этим сайтом
используется [spaceship](https://github.com/fastlane/fastlane/tree/master/spaceship).
Он логиниться на сайте, а затем мы используем его куки для дальнейших запросов.
