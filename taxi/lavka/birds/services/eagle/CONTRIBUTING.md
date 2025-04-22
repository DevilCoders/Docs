## Concept

*   Лавка.Орёл является FullStack TypeScript проектом.

*   Исходный код проекта хранится в папке `src` и компилируется в JavaScript код (папка `out`).

*   Для запуска скомпилированного JS необходимо:
    *   NodeJs соотв. версии
    *   `npm ci --only=prod`

*   Клиентский код живет в папке `src/client/`.

*   Библиотеки (пакеты, сервисы) расположены в папке `src/services/`.

*   Проект компилируется в папку `out/`:

    ```txt
    out/
    ├── client/
    ├── server/
    └── src/
    ```

    где:
    *   `client/` содержит все необходимые клиентские asset-ы
    *   `server/` содержит Express приложение
    *   `src/` содержит скомпилированный проект с сохраненной структурой файлов (нужно для тестов и cli команд)

### Проверить, как изменения в коде повлияли на бандл

1. Собрать бандл через `eagle webpack` команду с production окружением и параметром создания репорта
    ```bash
    NODE_ENV=production eagle webpack -n client --report
    ```

1. В `storage/temp/` появится директория с html отчетом и stat файлами
    ```bash
    ls -hl storage/temp/webpack-reports/client/ | cut -d\  -f8-

       48M Apr 15 12:07 eagle-client.html
      256B Apr 15 12:07 stats
    ```

1. Открываем отчет в браузере
    ```bash
    open storage/temp/webpack-reports/client/eagle-client.html
    ```
