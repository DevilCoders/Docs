## Манифесты
### Введение
```
dev:
  endpoints:
    subvention:
      calc_references:
      - migrated_clients
      - contracts
      - lock
      actions:
      # before_lock
      - stage:     before_lock
        reference: state_params
        name:      state_params
        method:    Lib.MakeMap
        params:
        - { action: const, value: client_id }
        - { action: get, key: input.Event.client_id }
        - { action: const, value: type }
        - { action: const, value: cutoff_dt_state }
    
      - stage:     before_lock
        reference: read_batch_params
        method:    Lib.MakeMap
        deps:
        - state_params
        params:
        - { action: const, value: states }
        - { action: get, keys: [references.state_params] }
    
      # lock
      - stage:  lock
        method: Accounter.CreateSharedLock
        params:
        - { action: get, key: references.account_location }
    
      # after_lock
      - stage:     after_lock
        reference: batch
        name:      batch
        method:    Accounter.ReadBatch
        params:
        - { action: get, key: references.read_batch_params }
    
      - stage:     after_lock
        reference: lock
        method:    Lib.MakeMap
        deps:
        - batch
        params:
        - { action: const, value: states }
        - { action: get, key: references.batch.States }
    
      # after_calc
      - stage:     after_calc
        reference: write_batch
        method:    Accounter.WriteCalculatorResponse
        params:
        - { action: join, keys: [input.Namespace, input.Endpoint], value: ":" }
        - { action: get, key: calc_result.Data.Event.transaction_id }
        - { action: get, key: calc_result.Data.Event.tariffer_payload.common_ts }
        - { action: get, key: calc_result.Data.Event }
        - { action: get, key: calc_result.Data.Transactions }
        - { action: get, key: references.account_location }
        - { action: get, key: lock_state.uid }
  calculator:
    transport:
      name: calculator-taxi
      debug: false
      baseUrl: "https://calculator.test.billing.yandex.net/taxi/v1"
      retries:
        count: 3
  queues:
      subvention:
        endpoint: "lbkx.logbroker.yandex.net"
        topic: "/billing/dev/subvention"
        consumer: "/billing/dev/subvention-consumer"
        tvmId: 2001059
        maxReadMessagesCount: 7
        handler:
          client: Processor
          errorProducer:
            endpoint: "lbkx.logbroker.yandex.net"
            topic: "/billing/dev/subvention-error"
            tvmId: 2001059
```

* `dev` — указание среды (dev, test, prod, load, ...)
* `endpoints` — ручки калькулятора. При обработки события, запрос будет отправлен в `${calculator.transport.baseUrl}/${endpoint}`
* `calculator` — настройки клиента калькулятора
* `queues` — настройки вычитывания сообщений из logbroker

### endpoints
Каждый endpoint состоит из следующих секций:
* calc_references — список references, которые должны быть переданы в калькулятор, чтобы ограничить кол-во передаваемых данных
* actions — массив операций
    * stage — этап. Возможные значения: `before_lock`, `lock`, `after_lock`, `before_calc`, `after_calc`
    * reference — название справочника. Пример: `foo` будет доступен в других action через `references.foo`
    * name — название. Должно быть уникальным в рамках stage.
    * method — метод, который нужно вызвать (см. ManifestAdaptor из billing/hot/processor/pkg/core/manifest/adaptor.go)
    * deps — зависимости, после каких action нужно выполнять этот action. Т.к. все action выполняются паралелльно, может сложиться ситуация, что используется значение, которое еще не вычислено. Для этого нужно выставить зависимости между этапами.
    * params — параметры, которые будут переданы в `method`.
        * action — действие, которое нужно сделать, чтобы сформировать параметр. Возможнные значения `get`, `const`, `set_null`, `join`, `get_column`
        * value — статичное значение, при action `const`
        * key, keys — ключи, которые необходимо извлечь из контекста
        * disallow_nil — запретить, чтобы параметр был nil
        * nullify_missing — если ключ отсутствует, проставить nil, вместо ошибки

Все actions обрабатываются паралельно в рамках одного stage.