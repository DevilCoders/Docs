# Калькулятор для BNPL(Buy now, pay later)

## Запуск локально

* ``~/arcadia/billing/hot/faas/python$ ya make --yt-store -D FUNCTION=billing.hot.bnpl_calculator.calculator.faas.adaptor.cashless -D FUNCTION_PEERDIR=billing/hot/bnpl_calculator/calculator``
  — биндинг cashless c FaaS;
* ``~/arcadia/billing/hot/faas/python$ ya make --yt-store -D FUNCTION=billing.hot.bnpl_calculator.calculator.faas.adaptor.payout -D FUNCTION_PEERDIR=billing/hot/bnpl_calculator/calculator``
  — биндинг payout с FaaS;
* ``~/arcadia/billing/hot/faas/python$ ./bin/faas check`` — проверка, что биндинг корректен;
* ``~/arcadia/billing/hot/faas/python$ ./bin/faas runserver`` — запуск локального сервера с функцией;
* ``$ curl 127.0.0.1:8080/ping`` — проверка сервера;
* ``$ 127.0.0.1:8080/call/raw`` — ручка для вызова одной из функций калькулятора **Яндекс.Оплат**.
