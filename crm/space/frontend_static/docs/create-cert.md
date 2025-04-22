## Создание сертификата

1. [Заказываем](https://crt.yandex-team.ru/certificates) сертификат
    ```
    CA name:         InternalCA
    Тип сертификата: Для web-сервера
    Хосты:           localhost.yandex-team.ru
    ABC-сервис:      CRM
    Common name:     localhost.yandex-team.ru
    Остальные поля не трогаем<
    ```
2. Скачиваем
3. Переименовываем в `local.pem`
4. Открываем сертификат в редакторе и копируем часть:

    ```
    -----BEGIN PRIVATE KEY-----
        <base64>
    -----END PRIVATE KEY-----
    ```
   в отдельный файл `local.key`

5. Кладем оба файла в `./.ssl`