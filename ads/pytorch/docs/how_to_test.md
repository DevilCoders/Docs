<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Как писать/запускать тесты](#%D0%BA%D0%B0%D0%BA-%D0%BF%D0%B8%D1%81%D0%B0%D1%82%D1%8C%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0%D1%82%D1%8C-%D1%82%D0%B5%D1%81%D1%82%D1%8B)
  - [Локальный запуск ручками](#%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D1%80%D1%83%D1%87%D0%BA%D0%B0%D0%BC%D0%B8)
  - [Локальный запуск через ya.make](#%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D1%87%D0%B5%D1%80%D0%B5%D0%B7-yamake)
  - [Запуск в yt через ya.make](#%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D0%B2-yt-%D1%87%D0%B5%D1%80%D0%B5%D0%B7-yamake)
- [Детали реализации](#%D0%B4%D0%B5%D1%82%D0%B0%D0%BB%D0%B8-%D1%80%D0%B5%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Как писать/запускать тесты

Юнит тесты на библиотеки можно запускать тремя (!) способами:
1. Самому ручками через pytest
2. Локально через ```ya make -rtA``` в ads_pytorch_test
3. В YT через ```ya make -rtA --run-tagged-tests-on-yt```

Интеграционные тесты ```ads_pytorch_integration_tests``` можно запускать только через ya.make, поскольку для них требуется поднятие локального ытя + некоторые тесты проверяют работоспособность связки аркадии + торча. К примеру, есть end2end тест запуска обучения из аркадии, обучения и inference результирующей модельки в C++ коде применялки.

## Локальный запуск ручками
Вам нужно настроить окружение на вашей виртуалке. Подробно об этом написано в документации про запуск моделей. Далее идете в директорию с вашим пакетом и дергаете pytest.

Помимо прочего, надо поставить pip'ом пакеты для тестов:
* pytest-xdist
* pytest-asyncio

Рассмотрим на примере ads_pytorch:
```(bash)
alxmopo3ov@ads-4v100:~/arcadia/ads/pytorch/packages/ads_pytorch$ tput reset && MKL_SERVICE_FORCE_INTEL=1 ADS_PYTORCH_BUILD_DIR=~/torch_build_dir python -W ignore -m pytest tests/hash_embedding/ -vv -n 20
```

Что здесь происходит:
1. ```tput reset``` - надежно чистит терминал от предыдущего мусора
2. ```MKL_SERVICE_FORCE_INTEL=1``` - какой-то странный костыль для нормальной работы cpu в кишках pytorch, уже и не помню, зачем точно нужен, но если убрать - может ругнуться
3. ```ADS_PYTORCH_BUILD_DIR=~/torch_build_dir``` - переменная окружения, указывающая, где будет кеш сборки C++ кода ads_pytorch. PyTorch использует систему сборки ninja, которая сама следит за изменениями в сорцах и пересборкой, от пользователя требуется лишь создать постоянную директорию, чтобы сборка C++ кода кешировалась и не приходилось ждать на каждый запуск тестов
4. ```python -W ignore -m pytest tests/hash_embedding/ -vv -n 20``` - запустить тесты в папочке ```tests/hash_embedding``` в 20 воркеров

## Локальный запуск через ya.make
**Не рекомендуется** запускать через ya.make юнит-тесты ```ads_pytorch_test```, потому что это сильно медленнее и менее удобно, чем локальный запуск руками выше. Локальные запуски через ya.make нужны только там, где тестируется связность с аркадией - это интеграционные тесты в ```ads_pytorch_integration_tests```. Для работы интеграционных тестов локально нужно доустановить пакеты:

```(bash)
pip install yandex-yt-local psutil pytest jsonschema
```

В остальном все предельно просто - запускаете командой ```ya make -rtA --test-stdout --test-stderr```.

Особенности:
1. Кеш сборки ads_pytorch будет **персистентный** и будет храниться по адресу ```packages/ads_pytorch/.yatest_build_cache```. Сделано это для быстрого запуска тестов, ждать по 2-3 минуты каждый раз на рекомпиляцию неудобно. Система сборки ninja сама разрулит все изменения в сорцах.
2. Стриминг stdout и stderr будет буферизованный. Я постарался отключить буферизацию везде, куда дотянулся, но куда-то не смог дотянуться. Кажется, где-то внутри ya.make запускаются свои подпроцессы в тестах, и там все еще включена буферизация. Из-за этого stdout и stderr будут выплевываться небольшими блобами.

## Запуск в yt через ya.make
Если вы не делаете **принципиально** новых тестов с новой настройкой окружения и т.п. - запускаться в yt вам **не нужно**.

Сейчас, чтобы запуститься локально в yt, недостаточно просто добавить команду ```--run-tagged-tests-on-yt```, нужно настроить спеку. Правильная спека для локального запуска выглядит как-то так:
```
{
    cluster=hahn;
    pool="alxmopo3ov";
    cypress_root="//home/ads/tzar/ci/tmp/ytexec";
    "operation_spec" = {
        "scheduling_tag_filter" = "porto";
        "pool_trees" = [
            "gpu_tesla_v100";
        ];
        "pool" = "nirvana-ads-deep-learning-ci";
    };
    "job_shells" = [
        {
            "name" = "N";
            "owners" = [
                "alxmopo3ov"
            ];
            "subcontainer" = "/N";
        }
    ];
    "task_spec" = {
        "gpu_limit" = 2;
        "cpu_limit" = 15;
        "cuda_toolkit_version" = "10.1";
        "layer_paths" = [
            "//home/ads/tzar/ci/porto_layers/layer_1_pytest_report";
            "//home/ads/tzar/ci/porto_layers/layer_2";
            "//home/ads/tzar/ci/porto_layers/layer_3";
            "//home/ads/tzar/ci/porto_layers/layer_4";
        ];
    };
}
```

Что изменилось:
1. ```pool="alxmopo3ov";``` говорит, что мы запускаемся от себя, а не от девтулзов.
2. ```"pool" = "nirvana-ads-deep-learning-ci";``` откуда будем брать ресурсы. Лучше бы брать их из нашей квоты
3. ```cypress_root="//home/ads/tzar/ci/tmp/ytexec";``` - указываем свой cypress root, к девтулзовому не будет доступа
4. ```"job_shells"``` включает возможность подssh-шиться к вашей джобе и поиграться с ней

**ОЧЕНЬ ВАЖНО:** при первых пристрелочных запусках было ощущение, что у запускалки ыть операций есть свой кеш в cypress_root. Как бы то ни было, рекомендуется **удалять cypress_root перед каждым запуском**. У меня без этого действия операции просто не запускались, тест молча бежал без ошибок.

Чтобы подssh-иться к джобе, нужно будет ввести команду ```yt --proxy hahn run-job-shell <<insert ur job id here>> --shell-name N```. JobID можно посмотреть в UI, зайдя в операцию во вкладку jobs.

# Детали реализации
Здесь и далее большинству пользователей читать необязательно, только core разработчикам.
