# Hermione

Тасклет для запуска [hermione](https://github.com/gemini-testing/hermione)-тестов в окружении [Sandbox'a](https://sandbox.yandex-team.ru).

Перед запуском пользовательской команды (указывается в `input.config.run_tests_cmd`) выполняется настройка окружения:
- установливаются переменные окружения, указанные пользователем (публичные и секретные из [yav](https://yav.yandex-team.ru/)). А так же системные: `SANDBOX_TASK_ID` и `SANDBOX_TASK_DIR`. Все эти переменные окружения будут доступны в пользовательской команде - `run_tests_cmd`;
- подготавливается рабочая копия - маунт аркадии.

Ожидается, что пользователь будет выставлять в [requirements](https://docs.yandex-team.ru/ci/requirement) свой контейнер, в который предустановлены [nvm](https://github.com/nvm-sh/nvm), [node](https://nodejs.org/en/), пакетный менеджер (например, [npm](https://www.npmjs.com/)) и другие инструменты. Затем внутри команды `run_tests_cmd` необходимо проинициализировать nvm (т.е. добавить путь до бинаря ноды в `PATH`), для возможности установки зависимостей (если не скачивается из ресурса) и после чего можно запустить `hermione`. В случае использования [Trendbox LXC-контейнера](https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci_recepty/trendbox_ci_sborka_kontejnera_lxc_.html) можно для инициализации nvm запустить команду - `source /etc/trendbox`. Подробнее в [тикете](https://st.yandex-team.ru/FEI-24741).

После запуска пользовательской команды сохраняются ресурсы, указанные пользователем в поле `input.config.result_resources`.

## Пользователям

Подробное описание тасклета с примерами его использования находится в [реестре задач](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/frontend).
