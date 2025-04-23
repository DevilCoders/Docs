```bash
lerna bootstrap --scope @yandex-taxi/callcenter-beta --include-dependencies
```

```bash
lerna add --scope @yandex-taxi/callcenter-beta <package-name>
```

#### Локальный запуск
0. Устанавливаем версию ноды на мажорную 12: `nvm install 12` или, если уже есть, `nvm use 12`
1. Устанавливаем зависимости `lerna bootstrap --scope @yandex-taxi/callcenter-beta --include-dependencies`
2. Создаём алиасы доменов в `/etc/hosts`:

    ```bash
    npm run hosts:alias
    ```
   
    И проверяем, что алиасы добавились в конец файла
3. Идём в https://crt.yandex-team.ru/certificates. Жмём "Заказать сертификат".
    Во всплывающем окне указываем:  
      * CA name - `InternalCA`,  
      * Тип сертификата - `Для web-сервера`,  
      * Хосты - `*.<username>.local.yandex.ru, *.<username>.local.yandex.by, *.<username>.local.yandex-team.ru`,  
      * ABC-сервис - `Сервисы Такси`. 
    
    Тут важно, что домен первого уровня должен быть `yandex`, чтобы браузер нормально отправлял куки сессии Паспорта.
4. Скачиваем `.pem` файл с сертификатом.
5. Кладём `.pem` файл в домашнюю директорию пользователя под именем `.server.pem`. Пример для MacOS: `/Users/<username>/.server.pem`.
6. Запускаем командой `npm start`.
7. Дожидаемся пока соберётся и выведет URL, на котором запустилось.
8. Чтобы ходить во внешнюю проксю нужно зайти сюда и добавить свой хост https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/CC_AUTHPROXY_CORS
9. Так как прокся проверяет права, то нужно либо завести учетку с правами, либо воспользоваться общей тестовой.
   Общая учетка - https://yav.yandex-team.ru/secret/sec-01ezywq6sfft0z3dn3sqtmeqr6/explore/versions
   
   Заведение оператора - https://tariff-editor.taxi.tst.yandex-team.ru/call-center/operators/create

#### Как сделать звонок в тестинге или dev
1) Нужно найти оператора в https://phoneorderbeta.taxi.tst.yandex.ru/admin/disp/tasks
и вывести его на очередь ru_taxi_test_on_99.
2) Выйти этим оператором в форме на линию
3) Позвонить на номер +74999290227

https://phoneorderbeta.taxi.yandex.ru/form/disp - диспетчерская
https://phoneorderbeta.taxi.yandex.ru/form/support - саппорты

В тестинге или dev форму диспетчерской можно открыть без звонка
https://phoneorderbeta.taxi.yandex.ru/form/disp?show_form=1


#### Формы саппортов
У сапорта есть две формы
1) Для водителей
2) Для пользователей

Основной интерфейс для формы саппорта расположен тут. Сама форма появляется при активном звонке:
https://phoneorderbeta.taxi.yandex.ru/form/support.
Какую форму открывать определяется по названию метаочереди на которую приходит звонок. 
Список для которых нужно открывать форму водителей расположен тут в поле driver_lines - https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/CALLCENTER_DRIVER_SUPPORT_FORM
   
Каждую форму можно открыть по отдельности

1) Водительская - https://phoneorderbeta.taxi.tst.yandex.ru/support-driver
2) Пользовательская - https://phoneorderbeta.taxi.tst.yandex.ru/support
