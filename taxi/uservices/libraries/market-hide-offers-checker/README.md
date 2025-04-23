# Market Hide Offers Checker Library

### Определение
Библиотека для определения наличия скрытия оффера. Работает на базе унифицированного файла скрытий и market-access:
- market-access отвечает за обновления ресурса (т.е. унифицированного файла скрытий)
- унифицированного файла скрытий содержит в себе список правил отвечающий за причины скрытий

### Дополнительная информация о зависимостях
- [унифицированные правила скрытий вики](https://wiki.yandex-team.ru/users/vlmarkov/minimarket-hide-offers-microservice/)
- [унифицированные правила скрытий сервис](https://a.yandex-team.ru/arcadia/taxi/uservices/services/market-hide-offers-dyn2yt/)
- [userver market-access](https://a.yandex-team.ru/arcadia/taxi/uservices/libraries/market-resource-updater/)

### API
- при интеграции этой библиотеки с вашим сервисом, сервис должен поддеражть следующий API
- [ссылка](https://a.yandex-team.ru/arcadia/taxi/schemas/schemas/services/market-hide-offers-rt/api/check_status.yaml)

### Как подключить библиотеку
1. Необходимо подключить ```ComponentList```:
    ```
    #include <market-hide-offers-checker/component_list.hpp>

    void RegisterUserComponents(components::ComponentList& component_list) {
        component_list.AppendComponentList(market_hide_offers_checker::ComponentList());
    }
    ```

2. Необходимо в модуле зависимостей найти ```Component```:
    ```
    class Dependencies {
        public:
            Dependencies(const components::ComponentConfig& config,
                         const components::ComponentContext& context);

        struct Extra {
            const market_hide_offers_checker::HideOffersChecker& offers_checker;
        };

        Extra GetExtra() const;

        private:
            const market_hide_offers_checker::HideOffersChecker& offers_checker_;
    };

    Dependencies::Dependencies(const components::ComponentConfig& config,
                               const components::ComponentContext& context) {
        offers_checker_ = context.FindComponent<market_hide_offers_checker::HideOffersChecker>());
    }

    Dependencies::Extra Dependencies::GetExtra() const {
        return {offers_checker_};
    }

    ```

3. Необходимо в ```service.yaml``` подключить библиотеку:
    ```
    libraries:
        - yandex-taxi-library-market-hide-offers-checker
    ```

4. Необходимо в ```config.user.yaml``` описать конфигурацию компонентов:
    ```
        market-hide-offers-checker:
            dir: $test_work_dir/uhor # test only
            abo-file: abo-file # test only
            mmap-file: mmap-file # test only
            fs-task-processor: fs-task-processor # test only
        resource-updater:
            enabled: $access_enabled
            task-processor: resource-updater-task-processor
            access-agent:
                customer: market-uaccess
                endpoint: localhost:2406
                poll_interval: 10s
                retry_interval: 10s
            fs-task-processor: fs-task-processor
        grpc-client-factory:
            task-processor: resource-updater-task-processor
    task_processors:
        resource-updater-task-processor:
            thread_name: resource-updater-worker
            # Небольшое число тредов, соединения должны создаваться редко
            worker_threads: 1
    ```
5. Ипользование в API обработчике:
    ```
    Response View::Handle(Request&& request, Dependencies&& dependencies) {
        const auto& offers_checker = dependencies.extra.offers_checker;
        const auto response = offers_checker.Process(request);
        return Response200{response};
    }
    ```


### Пример использования
- [сервис скрытий runtime](https://a.yandex-team.ru/arcadia/taxi/uservices/services/market-hide-offers-rt/)

### Как сборать библиотеку
```
~/arcadia/taxi/uservices/libraries/market-hide-offers-checker$ ../../../../ya make
```

### Как тестировать
- внутренних тестов реализация не предусматривает, т.к. это обертка над:
  - market-resource-updater
  - unified-hide-offers-library
- тесты предусмотрены в использующем сервисе см. раздел ```пример использования```
