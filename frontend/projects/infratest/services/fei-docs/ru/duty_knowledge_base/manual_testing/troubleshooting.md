# Troubleshooting [Manual Testing]

## Почему не запустилась раздача тест-ранов на ассесоров в релизе?

1. Переходим в SEAREL-тикет (например, [SEAREL-14560](https://st.yandex-team.ru/SEAREL-14560)). Ищем комментарий от робота @robot-eksperimentus. Это пользователь, который автоматизирует процессы AB. Робот не наш. В комментарии есть ссылка на Sandbox-таск `AB_DEPLOYING_RUN_TESTS`.
![](https://jing.yandex-team.ru/files/dudkevich/ab_deploying_task.png)
2. Смотрим на время создания и запуск таска. Если оно приблизительно совпадает с тем, когда создан SEAREL-тикет, то идём дебажить дальше, иначе идём в [Экспериментальный чатик](../kanaly_i_rassylki.md) с вопросом о том, что не так.
3. В дочерних тасках есть `AB_DEPLOYING_TEST_ASSESSORS`, которая запускает другую таску — `SANDBOX_CI_TESTPALM_SUITE_RUNNER`. Эта таска создаёт тест-раны в проекте. Смотрим на её время. Если время близкое с временем запуска родительской таски, то дебажим дальше.
4. В таске забираем значение параметра `testpalm_project_suffix` — это проект в TestPalm (например,
`issue-searel-14560`). Переходим в него (пример ссылки - `https://testpalm2.yandex-team.ru/serp-js-issue-searel-14560`). Далее на вкладку «Test Runs». Там должны быть созданные тест-раны. Скорее всего они называются «оригинальные тест-раны». Забираем идентификатор любого тест-рана.
![](https://jing.yandex-team.ru/files/dudkevich/test_run_version.png)
5. Переходим в [сервис accessors_gate_stable в Deploy](https://deploy.yandex-team.ru/stage/assessors_gate_stable/logs?deploy-unit=api) и выполняем поиск по `message=<test_run_id>`. Если данных нет, то необходимо выполнить запрос через YQL. Смотрим время создания Sandbox-таски — в логе будет `sandbox task successfully started`. Если время приблизительно совпадает со временем создания Searel-тикета (+/- 5 минут), то дебажим дальше, иначе обращаемся в [поддержку TestPalm](https://forms.yandex-team.ru/surveys/47384/), что сервис долго не отправлял фидбек о создании тест-рана через механизм раннеров (раннер — `BulkCurlRunner`).
6. Дальше лучше позвать эксперта.

## Я не нашел ответ на свой вопрос

Попробуйте найти решение на [wiki](https://wiki.yandex-team.ru/search-interfaces/infra/assessors/#m-dezhurstvo). Если не нашли, то обратитесь к эксперту.
