## Системные тесты NWSMTP(deprecated)
Запускаются против стенда и заданных хостов.

### Доступы:
С машинки, откуда запускаются тесты, необходимо иметь доступы:

1. до _C_MAIL_QA_MXS_, порты 25, 27, 2000, 22 (доступ до nwsmtp, nwsmtp-out, МХ-серверов и ssh-доступ для use_ssh_proxy) 
2. до exchange-2013.yandex-team.ru, порт 993 (для тестов на exchange)
3. доступ на чтение для секрета https://yav.yandex-team.ru/edit/sec-01cycce5e6j67n3tjs89v5bmsg

### Организация тестов:
Все тесты разделены по папкам по функциональному признаку. Каждый тест помечается типом бекенда против которого доступен его запуск. Для других типов бекенда тест будет заскипан.

    
### Запуск тестов

Если после запуска возникает вот такя ошибка `Outdated RSA signature. \u0421heck and synchronize the local time on the computer`
То надо сделать так: `sudo sntp -sS time.apple.com`

1. Запускаются тесты командой:
   
   (в данном случае из директории ./mxtests)
    
    ```bash
    ./mxtests -m pytest -E qa -M bigmail -B mxback ./tests
    ```    
    `-E` - выбор типа окружения
     
     Посмотреть список поддерживаемых окружений можно так:

   ```bash
   ./mxtests -m pytest -E sdfdsfdsf
   usage: pytest [options] [file_or_dir] [file_or_dir] [...]
   pytest: error: argument -E: invalid choice: 'sdfdsfdsf' (choose from 'qa', 'testing', 'corp')
      ```
      
      `-M` - выбор типа почты: большая bigmail или corp;
      
      `-B` - выбор типа бекенда

   Посмотреть список поддерживаемых типов можно так:
    
   ```bash
    ./mxtests -m pytest -B ololo ./
    usage: pytest [options] [file_or_dir] [file_or_dir] [...]
    pytest: error: argument -B: invalid choice: 'ololo' (choose from 'mxcorp', 'mxback', 'mxfront', 'smtp', 'yaback', 'mxbackcorp', 'smtpcorp')
   ```
   
   Если требуется сделать распараллеленный запуск всех тестов, то выполняем команду:
    ```bash
    ./mxtests -m pytest -E qa -M bigmail -B mxback ./tests/ -n 8
    ```

2. Запуск тестов в тестинге:
    ```bash
    ./mxtests -m pytest -E testing -M bigmail -B mxback ./tests
    ```  

3. Запуск напротив QA-сервера: 
- нужно перед выполнением py.test -E qa -M bigmail -B mxback ./tests  в файле properties.qa.bigmail.yml указать пароль от pq-базы вместо ххххххх:
    ```yaml
    xdb:
      user: "mxback"
      pwd: "xxxxxxxxx"
      ssh_proxy_host: "mxback-qa2.cmail.yandex.net"
    ```
    *Перед запуском тестов настоящий пароль от базы можно посмотреть на тестовых мх-хостах в /etc/yamail/.pgpass*
    
4. Запуск тестов на корпе:
    ```bash
    ./mxtests -m pytest -E qa -M corp -B mxback ./tests -n 8
    ```
    Аналогично (3) в файле properties.qa.corp.yml придется указать пароль от pq-базы.
 
5. Переопределить хост и порт можно так:
    ```bash
    ./mxtests -m pytest -M bigmail -B mxback --host mxback-sandbox.mail.yandex.net --port 1234 ./tests/test_plus_after_login.py
    ```

### Генерация отчетов

По завершению выполнения тестов нужно выполнить команду:
   ```
    allure generate --clean  -o ./html ./report
   ```
   Затем нужно поискать в папке html файлик index.html - это полный отчет.
   Открывать его желательно в браузере FireFox.
