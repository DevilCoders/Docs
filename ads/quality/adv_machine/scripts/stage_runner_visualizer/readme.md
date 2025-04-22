# Stage runner visualizer #

Рисует графики stage runnera

Поддерживается 2 режима
- draw-priemka (рисует графы по дампу приемки)
- draw-daemon (рисует графы по конфигу)


В оба режима можно опционально подать select_type.json и service (для поиска) / stand version (для РСЯ).
В этом случае стадии мерджатся и подтягиваются параметры из cgi в UseRequestParams.

## Пример запуска draw daemon
- search-apphost [Граф](https://jing.yandex-team.ru/files/ekondranin/daemon.svg)
> ./stage_runner_visualizer draw-daemon -d daemon.json -s select_type.bin --service adv-machine-search-apphost -o daemon

- search-apphost (без select type) [Граф](https://jing.yandex-team.ru/files/ekondranin/daemon_simple.svg)
> ./stage_runner_visualizer draw-daemon -d daemon.json -o daemon_simple

- offer-retargeting [Граф](https://jing.yandex-team.ru/files/ekondranin/daemon_rsya.svg)
> ./stage_runner_visualizer draw-daemon -d daemon_rsya.json -s select_type.bin --stand-version 42 -o daemon_rsya

## Пример запуска draw priemka
- monoindex [Граф](https://jing.yandex-team.ru/files/ekondranin/monoindex.svg)
> ./stage_runner_visualizer draw-priemka -c files.json -s select_type.bin --service adv-machine-monoindex-apphost -o monoindex

- monoindex (без select type) [Граф](https://jing.yandex-team.ru/files/ekondranin/monoindex_simple.svg)
> ./stage_runner_visualizer draw-priemka -c files.json -o monoindex

files.json

    {
        "Files": [
            {
                "Filename": "monoindex_dump.json",
                "SimDistances": [25, 100025, 700025, 800025]
            }
        ]
    }


Подготовка лога (**важно!** - не должно быть таймаутов)

> ./am_priemka apphost_shelling -o monoindex_dump.json --service-id adv-machine-monoindex-apphost -a ammo.json -m meta_monoindex.json -R 100 -t 30000 -c 1000

- search + rm + dsa [Граф](https://jing.yandex-team.ru/files/ekondranin/search.svg) (предполагается, что daemon.json и параметры 3 эксперимента совпадают)
> ./stage_runner_visualizer draw-priemka -c files.json -s select_type.bin --service adv-machine-search-apphost -o search

files.json

    {
        "Files": [
            {
                "Filename": "search_dump.json",
                "SimDistances": [25]
            },
            {
                "Filename": "rm_dump.json",
                "SimDistances": [100025]
            },
            {
                "Filename": "dsa_dump.json",
                "SimDistances": [700025]
            }
        ]
    }
Подготовка лога
> ./am_priemka apphost_shelling -o search_dump.json --service-id adv-machine-search-apphost -a ammo.json -m meta_search.json -R 100 -t 30000 -c 1000
>
> ./am_priemka apphost_shelling -o rm_dump.json --service-id adv-machine-rm-apphost -a ammo.json -m meta_search.json -R 100 -t 30000 -c 1000
>
> ./am_priemka apphost_shelling -o dsa_dump.json --service-id adv-machine-dsa-apphost -a ammo.json -m meta_search.json -R 100 -t 30000 -c 1000