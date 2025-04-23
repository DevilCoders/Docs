# Админка market-loyalty

### Локальный запуск

Из корня репозитория:

```bash
cp market-loyalty-admin/src/main/properties.d/local/local.properties.ex market-loyalty-admin/src/main/properties.d/local/local.properties
./gradlew -Plocal :market-loyalty-admin:run
```

  или если нужен запуск in-memory postgresql

```bash
./gradlew -Plocal -Pinmem :market-loyalty-admin:run
```

Админка должна подняться на порту 8081.

#### Особенности локального запуска на Windows

Для запуска на Windows 10 удобнее использовать вариант с пропуском тестов:
```
./gradlew.bat -x test -Plocal -Pinmem :market-loyalty-admin:run
./gradlew.bat -x test -Plocal :market-loyalty-admin:run
```
Предварительно в **local.properties** нужно указать пароль для подключения к БД
```
pgaas_password_rw=postgres
pgaas_password_ro=postgres
```

#### База данных для локального запуска
При запуске с флагом `-Pinmem` поднимается embedded БД с той структурой/данными, которые прописаны в ликвибейзе. Если есть желание и необходимость, можно поднять постоянный локальный инстанс PG и запускать без флага.

#### Отключить валидацию кук
При запуске с флагом `-Plocal` отключается проверка паспортных кук, что позволяет запускать приложение локально.

#### Включить TMS для локального запуска
При запуске с флагом `-Ptms` включается TMS (которая отключена по-умолчанию для локального запуска).

#### Включить оптимизацию javascript
При запуске с флагом `-Poptjs` включается оптимизация javascript при сборке (которая отключена по-умолчанию для локального запуска).

#### LiveEdit
1. Запускаем приложение (:market-loyalty-admin:run)
2. Запускаем ../market-loyalty-admin-ui/devServer.sh, откроется страница в браузере на http://localhost:9000. Все запросы к api/** будут перенаправляться на 8081  
Теперь при любом изменении ../market-loyalty-admin-ui/src/\*\*/\* автоматически персобирается и страница перезагружается. 

### Настройка IntelliJ IDEA

#### Включение TSLint
1. Открыть **Settings...** > **Languages & Frameworks** > **TypeScript** > **TSLint**
2. Поставить галочку в **Enable**
3. Проверить, что указан путь до интерпретатора node (например, _~/repo/market-loyalty/market-loyalty-admin-ui/.gradle/nodejs/node-v10.16.0-linux-x64/bin/node_)
4. Проверить, что указан путь до пакета TSLint (например, _~/repo/market-loyalty/market-loyalty-admin-ui/node_modules/tslint_)

### Полезные плагины
1. [Angular state inspector (Chromium-based browsers)](https://chrome.google.com/webstore/detail/angular-state-inspector/nelkodgfpddgpdbcjinaaalphkfffbem?hl=en)
2. Augury [(Firefox)](https://addons.mozilla.org/en-US/firefox/addon/angular-augury/), [(Chromium-based)](https://chrome.google.com/webstore/detail/augury/elgalmkoelokbchhkhacckoklkejnhcd?hl=en)

### Отключение запуска `enableProdMode()`

В параметрах открытия страницы дополнительно передать `?prodMode=false`, например, если запущено локально с опциями 
`-Plocal -Poptjs`, то урл для админки будет выглядеть так: http://localhost:8081/?prodMode=false.
