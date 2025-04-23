### Запуск тестов

PYTEST_ADDOPTS="--morda_env=rc --tests_path=tests/kote/tests/olympiad/test_olympiad.yaml" PYTHONWARNINGS="ignore:Unverified HTTPS request" ya make -rA --test-disable-timeout --show-passed-tests --test-stderr 


### Ручное обновление данных
1) cd arcadia/portal/main/function_tests
2) make schemas
3) ya upload --do-not-remove --tar schema
4) прописываем resourse_id в [макрос DATA](https://a.yandex-team.ru/arcadia/portal/function_tests/tests/ya.make#L8)

### TODO
Сделать машинерию для обновления данных
