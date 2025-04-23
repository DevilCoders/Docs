## Запуск регрессии

В ходе регрессии будут использоваться секреты из [Yav](https://yav.yandex-team.ru). 
Для авторизации в Yav его клиент будет использовать токен из переменной окружения `YAV_OAUTH`, либо локальные данные пользователя.

Существует несколько способов запуска тестов:

1. В Sandbox. 
  
    Предварительно: 
    
    * Проверьте, что есть у вас доступ к секрету [sec-01dzxezq856wf8s37s8ndxyf8e](https://yav.yandex-team.ru/secret/sec-01dzxezq856wf8s37s8ndxyf8e/).
    * Пропишите в [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault) секрет с именем `ARC_TOKEN`, содержимым должен быть токен Arc (обычно доступен в `$HOME/.arc/token`).
    
    В [планировщике](https://sandbox.yandex-team.ru/scheduler/19622/view) нажимаем кнопку **Run once** и дожидаемся окончания.

    Результаты запуска тестов видны на вкладке `Tests Result` прямо на странице задачи.

2. Локально* с помощью безголового браузера. 

    Для этого локально должен быть установлен Chrome и Chromedriver (устанавливать здесь  `/usr/local/bin/chromedriver`) 
    
    `$ pytest -m "regression" ./src/tests/regression/`
   
3. Локально*, используя ферму Selenium. 

    Если chromedriver не установлен, то тесты попробуют сходить в [ферму браузеров](https://wiki.yandex-team.ru/selenium/). 
    
    Для запуска тестов нужно, чтобы были заказаны доступы от агента и до фермы `sg.yandex-team.ru:4444`, и от сети фермы `_SELENIUMGRIDNETS_`.
    Заказать доступы можно в [Puncher](https://puncher.yandex-team.ru).

4. Локально* со сборкой.

    Способ приближен к тому, что делается в Sandbox.
    
    `$ ya make -ttt`

\* При локальном запуске обязательно должен быть доступ с локальной машины до тестируемого сервиса `balalayka-test.paysys.yandex-team.ru:443`
