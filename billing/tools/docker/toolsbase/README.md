# Образ контейнера со всем необходимым чтобы запустились наши юнит-тесты
Собрать его просто: docker build . и всё готово. Готовый образ можно стянуть тут: registry.yandex.net/balance/toolsbase

# Использование контейнера
В контейнере не предусмотрено никакой входной точки, потому как запуск тестов дело индивидуальное. 
Для примера можно запустить вот так: 
```bash
docker run -ti --rm --name toolsbase -v ~/tools:/tools -v ~/utils:/utils registry.yandex.net/balance/toolsbase /tools/bin/billing-tests.sh -x -v
``` 
Это запустит все тесты баланса при условии что всё правильно у вас настроено. 
Поскольку запуск не требует запуска ./debug-confugre, то надо скопировать balance/balance-test.cfg.in в balance/balance-test.cfg.
И поправить его чтобы он смотрел в базу `DEV_BALANCE_YANDEX_RU`, а логи писал локально: `<Log level="info">balance-test.log</Log>`
