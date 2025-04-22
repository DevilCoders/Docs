## Разворачивание phf

### Запустить тесты

Только юнит-тесты
```bash
$ make test
```

Все тесты, включая интеграционные, которые общаются с direct-sandbox, blackbox и cryptaApi
```bash
$ DIRECT_TEST_TOKEN=<direct_token> DIRECT_TEST_CLIENT=<direct_client> CRYPTA_TOKEN=<crypta_token> make test-all
```
Чтоб получить _crypta_token_ нужно для yandex-team аккаунта в OAUTH получить доступ к Яндекс.Крипта. 

Сейчас _crypta_token_ есть у zomb-distribution@yandex-team.ru.

Чтоб получить _direct_token_ нужно 
* завести _direct_client_ на yandex.ru домене. 
* завести для клиента аккаунт в direct
* включить в аккаунте доступ к sandbox
* в OAUTH включить использование DirectAPI
* возможно, в direct еще нужно сделать заявку на тестовый доступ (не уверена)