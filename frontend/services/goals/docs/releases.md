# Релизы GOALS
1. Заполнить [форму](https://forms.yandex-team.ru/surveys/50569/?default_branch=master&service=goals&reason=unplanned).

    Что произойдет при отправке формы:
    1. Поднимется версия в package.json.
    2. Закоммитятся изменения, запушится коммит с версией в master.
    3. Отведется релизная ветка вида `release/goals/v<version>`.
    4. На событие пуша ветки в трендбоксе автоматически запустятся проверки, сборка образа, деплой в тестинг и препрод.
    5. Создастся релизный тикет в очереди [GOALS](https://st.yandex-team.ru/GOALS). [Список релизных задач в Трекере](https://st.yandex-team.ru/GOALS/order:updated:false/filter?resolution=empty()&type=release)
    6. После завершения всех проверок, в релизный тикет добавится комментарий с их статусами.

      - [Подробнее о том, как работает форма.](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/docs/faq/release-form.md)

      - [Sandbox-задачи на релиз, созданные формой](https://sandbox.yandex-team.ru/tasks?children=true&tags=goals&desc_re=релиз&limit=20&created=14_days)

  1. Когда релиз задеплоится в https://goals.test.yandex-team.ru/ ([testing](https://deploy.yandex-team.ru/stages/tools_goals_testing)), бот напишет в слак-канал [goals-duty](https://yndx-search.slack.com/archives/C01EPR7TJ2V) и призовёт тестировщика.

  2. Если нашлись баги, вмержить фикс в `master` и отвести релиз заново. При этом старый релиз закроется как "Некорректный".
  **Альтернативный вариант**: влить фикс в мастер и черри-пикнуть коммит с фиксом в релизную ветку, после чего запушить её — автосборка сработает заново автоматически.

  5. Если багов нет, перевести задачу в статус **«Протестировано»**.

  6. Выкатить релиз в [production](https://deploy.yandex-team.ru/stages/tools_goals_prod) (https://goals.yandex-team.ru/). Для этого нужно перевести тикет в статус "Выкатить в прод". Скрипт под капотом из релизной ветки выполнит команду `npm run ci:deploy:release:end`: это проставит релизный тег, удалит релизную ветку (с сервера), закроет релизную задачу и выкатит образ в продакшен окружение
