## Testcop

Для skip/mute тестов используется сервис Testcop.
[Документация сервиса](https://doc.yandex-team.ru/si-infra/tests-stability/overview.html).

### Settings

Настройка проекта в Testcop осуществляется на [странице конфигурации](https://testcop.si.yandex-team.ru/config/travel-frontend-portal).

### Skipped/muted tests

Актуальный список skip/mute тестов можно увидеть в [Testcop](https://testcop.si.yandex-team.ru/skips/hermione/travel-frontend-portal).

Список задач на починку тестов в [ST](https://st.yandex-team.ru/issues/?_o=updated+DESC&_f=type+priority+key+summary+description+status+resolution+updated+assignee+parent&components=%5B113633%5D&queue=%5B%22TRAVELFRONT%22%5D&resolution=%5B%22empty%28%29%22%5D).

[История skip/mute автотестов](https://testcop.si.yandex-team.ru/history/hermione/travel-frontend-portal)

### How skip/mute test

Заскипать или замьютить тест можно из sandbox задачи прогона тестов.
Для этого надо перейти в Testcop (бейдж с тайтлом `Testcop GUI`)

![testcop button in CI Flow](https://jing.yandex-team.ru/files/isaven/Untitled.9e41745.png)

В интерфейсе Testcop нужно выставить переключатель в новый статус (skip/mute/enable) напротив нужных тестов.
И нажать кнопку `Submit`

![testcop ui](https://jing.yandex-team.ru/files/isaven/Untitled%202.2c6cb5b.png)

В открывшемся модальном окне можно создать тикет на починку.

![issue modal](https://jing.yandex-team.ru/files/isaven/Untitled%202.3c21e69.png)

Для создаваемых тикетов используется [шаблон задачи Startrek](<https://st.yandex-team.ru/settings/templates/issues?name=Testcop%3A%20починка%20hermion-теста%20(шаблон%20по%20умолчанию)&owner=1120000000202633&queue=TRAVELFRONT>).
