## Клиент для juggler

### Запуск тестов
Для проверки с моками requests
```bash
$ ya make -tA
```

С походом в реальное API juggler
```bash
$ ya make -tA --test-param real_juggler=true
# при этом ответы juggler можно посмотреть вот тут
$ less tests/test-results/py3test/testing_out_stuff/stdout
```