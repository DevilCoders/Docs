# Как создать быструю нагрузку на выплаты в тесте
С помощью интеграционного теста `billing/hot/integration/taxi/test_many_requests`:
 - Пойти в `billing/hot/tests`
 - Добавить в Makefile параметр запуска только одного нужного нам теста:
```
-      ya make -A --test-tag=ya:manual -k $(params)
+      ya make -F taxi.test_many_requests.py -A --test-tag=ya:manual -k $(params)
```
 - Убрать skip перед нужным тестом:
```
-@pytest.skip
 def test_many_payouts(create_state_builder, payout_client, accounts_client):

```
 - Запустить make test

Чтобы у выплат были неттинги или CPF'ы надо добавить аргумент `with_netting=True` или `with_cpf=True` в функцию `write_batch`
