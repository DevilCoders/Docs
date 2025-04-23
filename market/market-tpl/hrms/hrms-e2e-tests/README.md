# HRMS E2E TESTS
Энд-ту-энд тесты HRMS

## Запуск локально с генерацией отчета

Обычно делается из консоли примерно так:

`ya make -ttt  -F '*e2etests.login*' --allure=allure-results/report --jvm-args '-Dhrms.user=<логин> -Dhrms.password=<пароль>'`

Либо можно прописать пользователя в ya.make

`
-Dhrms.user={user}
-Dhrms.password={password}
`

Тестовый пользователь для автотестов: `robot-market-hrms-at`
Пароль в секретнице: https://yav.yandex-team.ru/secret/sec-01g04jn6f0k1tmrarvad529x7f/explore/versions

Фильтр для запуска может быть любым, например `*e2etests.TrivialTest*`

Но нужно помнить о том, что фильтр должен трактоваться однозначно, потому как к примеру фильтр `*Test*` запустит все тесты в проекте т.к. это слово содержится в пути самого проекта.
