renderer-templates-ci-flows
===========================

Набор рецептов для генерации различных флоу, связанных с рендерера для аркадийного CI.

На данный момент реализовано 3 "рецепта":

- `main` - основной рецепт, в котором отражен общий способ раскатки шаблонов рендерера
- `lenour` - рецепт с мягким переключением, который, например, используется для релизов web4
- `rctemplates` - рецепт для залития обновлений на приемку

Все рецепты могут сосуществовать в рамках одного флоу и иметь общие точки синхронизации.

Пример конфигурации для параллельной раскатки общим рецептом и рецептом lenour:

```ts
// Результат во flows совместим по структуре с ожидаемой Arcadia CI в одноименном поле a.yaml.
// Предполагается, что далее он будет некоторым образом объединен с существующими a.yaml.
const flows = generateFlows({
    flows: {
        "readme-example": { // Джобы будут добавляться во флоу с таким названием
            jobsPrefix: "renderer", // Все джобы в рамках данного флоу будут иметь такой префикс
            clusters: [
                {
                    name: "web-main", // Имя кластера, включается в имена-идентификаторы джобов
                    recipe: { // Рецепто-специфичные опции, соседние опции являются общими
                        type: "lenour",
                        options: {
                            resourcesTrackerServiceId: "renderer_main_sas_test_prestable",
                            // На данный момент ленор-рецепт поддерживает единственный ресурс, поскольку необходимости в нескольких пока не возникало
                            resource: {
                                type: "WEB_MICRO_PACKAGE",
                                previous: {
                                    path: "previous-templates-web4.tar.gz",
                                },
                                latest: {
                                    path: "latest-templates-web4.tar.gz",
                                },
                                nextId: "${tasks.build.resource}",
                            },
                            lenourServices: {
                                lenour_sas_prestable_test: { label: "prestable" },
                                lenour_sas_stable_test: { label: "sas" },
                                lenour_vla_test: { label: "vla" },
                            },
                            // В ленор-рецепте локи на все локации берутся одновременно
                            locks: [
                                { name: "sas", path: "web/sas", actionId: "renderer_ci_web_sas_test" },
                                { name: "vla", path: "web/vla", actionId: "renderer_ci_web_vla_test" },
                                { name: "man", path: "web/man", actionId: "renderer_ci_web_man_test" },
                            ],
                            // Также есть возможность указать локи шаблонов, которые будут взяты до внесения каких-либо изменений в сервисы и отпущены по окончании всех обновлений
                            templatesLock: {
                                name: "web",
                                path: "web/templates",
                                actionId: "renderer_ci_web_templates_test",
                            },
                        },
                    },
                    services: {
                        renderer_main_sas_test_prestable: { label: "sas", alias: "sas-prestable" },
                        renderer_main_sas_test_stable: { label: "sas", alias: "sas-stable" },
                        renderer_main_vla_test: { label: "vla" },
                    },
                    prepareRecipe: "dynamic resource preparation",
                    activateRecipe: "dynamic resource activation",
                    // Дополнительно можно указывать в зависимостях список джобов, которые ожидаются в существующем ямле
                    needs: ["deploy"],
                },
                {   // Пример simple-рецепта
                    name: "lowload",
                    recipe: {
                        type: "simple",
                        options: {
                            activateOrder: [
                                // Подразумевает возможность указать порядок, в котором будут активироваться разные группы сервисов.
                                // Никакого дополнительного значения метки не имеют, могли бы быть произвольными, но они должны соответствовать ключам из объекта services.
                                // Здесь же можно описать необходимые локи, как ручные, так и локи от марти
                                {
                                    labels: ["sas"],
                                    // Локи на уровне этого рецепта также поддерживаются, но при одновременной раскатке при необходимости локов,
                                    // следует указывать их только в одном рецпте, если они пересекются.
                                    // locks: [
                                    //     {
                                    //         name: "sas",
                                    //         path: "web/sas",
                                    //         actionId: "renderer_ci_web_sas_test",
                                    //     },
                                    // ],
                                    manualLock: { name: "sas" },
                                },
                                {
                                    labels: ["vla", "man"],
                                    // locks: [
                                    //     {
                                    //         name: "rest-vla",
                                    //         path: "web/vla",
                                    //         actionId: "renderer_ci_web_vla_test",
                                    //     },
                                    //     {
                                    //         name: "rest-man",
                                    //         path: "web/man",
                                    //         actionId: "renderer_ci_web_man_test",
                                    //     },
                                    // ],
                                    manualLock: { name: "rest" },
                                },
                            ],
                            templates: [
                                {
                                    type: "WEB_LOWLOAD_MICRO_PACKAGE",
                                    path: "templates-web4-lowload.tar.gz",
                                    // id берется из априорного знания в какой джобе существующего флоу получается ресурс
                                    id: "${tasks.build.resource}",
                                },
                            ],
                            // Общий лок на рецепт, такой же как для lenour-рецепта. Также не следует брать одновременно с lenour
                            // templatesLock: {
                            //     name: "web",
                            //     path: "web/templates",
                            //     actionId: "renderer_ci_web_templates_test",
                            // },
                        },
                    },
                    services: {
                        renderer_sas_test_prestable: { label: "sas", alias: "sas-prestable" },
                        // Можно дополнительно указать алиас (в данном случае stable), в случае, если среди тех сервисов,
                        // которые необходимо активировать одновременно, более одного сервиса.
                        renderer_sas_test_stable: { label: "sas", alias: "sas-stable" },
                        renderer_vla_test: { label: "vla" },
                        renderer_man_test: { label: "man" },
                    },
                    prepareRecipe: "dynamic resource preparation",
                    activateRecipe: "dynamic resource activation",
                },
            ],
            // Опция syncJobs позволяет указать какие из джобов в рецептах следует синхронизировать.
            // Предполагается, что их названия являются публичным контрактом, предоставляемым рецептом
            // (префикс + название кластера + название джобы)
            syncJobs: [
                {
                    name: "sync-commits",
                    title: "Synchronize clusters commits",
                    jobs: ["renderer-web-main-all-committed", "renderer-lowload-committed"],
                },
                {
                    name: "sync-done",
                    title: "Synchronize clusters done",
                    jobs: ["renderer-lowload-done", "renderer-web-main-done"],
                },
            ],
        },
    },
}
```

<details><summary>Результат будет такой: (раскрыть)</summary>
<p>

```json
{
    "readme-example": {
        "renderer-web-main-init": {
            "title": "Init \"web-main\"",
            "task": "dummy",
            "needs": [
                "deploy"
            ]
        },
        "renderer-web-main-acquire-templates-lock-web": {
            "title": "Acquire lock renderer_ci_web_templates_test(web/templates)",
            "task": "projects/canti/canti_lock",
            "needs": [
                "renderer-web-main-init"
            ],
            "input": {
                "config": {
                    "action_id": "renderer_ci_web_templates_test",
                    "path": "web/templates",
                    "priority": 0
                }
            }
        },
        "renderer-web-main-get-previous-resource-id": {
            "title": "Get current \"WEB_MICRO_PACKAGE\" id from \"renderer_main_sas_test_prestable\"",
            "task": "projects/lenour/nanny_get_resource",
            "needs": [
                "renderer-web-main-acquire-templates-lock-web"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_prestable",
                    "resource_type": "WEB_MICRO_PACKAGE",
                    "local_path": "latest-templates-web4.tar.gz"
                }
            }
        },
        "renderer-web-main-get-previous-template-version": {
            "title": "Get template version from resource #${tasks.renderer-web-main-get-previous-resource-id.state.resource_id}",
            "task": "projects/lenour/get_template_version_from_resource",
            "needs": [
                "renderer-web-main-get-previous-resource-id"
            ],
            "input": {
                "config": {
                    "resource_id": "${tasks.renderer-web-main-get-previous-resource-id.state.resource_id}"
                }
            }
        },
        "renderer-web-main-get-latest-template-version": {
            "title": "Get template version from resource #${tasks.build.resource}",
            "task": "projects/lenour/get_template_version_from_resource",
            "needs": [
                "renderer-web-main-acquire-templates-lock-web"
            ],
            "input": {
                "config": {
                    "resource_id": "${tasks.build.resource}"
                }
            }
        },
        "renderer-web-main-commit-data-prepared": {
            "title": "\"web-main\" commit data prepared",
            "task": "dummy",
            "needs": [
                "renderer-web-main-get-previous-template-version",
                "renderer-web-main-get-latest-template-version"
            ]
        },
        "renderer-web-main-sas-prestable-commit-previous": {
            "title": "Commit resources to \"renderer_main_sas_test_prestable\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-web-main-commit-data-prepared"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_main_sas_test_prestable",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "previous-templates-web4.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.renderer-web-main-get-previous-resource-id.state.resource_id}"
                    }
                ]
            }
        },
        "renderer-web-main-sas-prestable-commit-latest": {
            "title": "Commit resources to \"renderer_main_sas_test_prestable\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-web-main-sas-prestable-commit-previous"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_main_sas_test_prestable",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "latest-templates-web4.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.build.resource}"
                    }
                ]
            }
        },
        "renderer-web-main-sas-stable-commit-previous": {
            "title": "Commit resources to \"renderer_main_sas_test_stable\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-web-main-commit-data-prepared"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_main_sas_test_stable",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "previous-templates-web4.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.renderer-web-main-get-previous-resource-id.state.resource_id}"
                    }
                ]
            }
        },
        "renderer-web-main-sas-stable-commit-latest": {
            "title": "Commit resources to \"renderer_main_sas_test_stable\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-web-main-sas-stable-commit-previous"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_main_sas_test_stable",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "latest-templates-web4.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.build.resource}"
                    }
                ]
            }
        },
        "renderer-web-main-vla-commit-previous": {
            "title": "Commit resources to \"renderer_main_vla_test\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-web-main-commit-data-prepared"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_main_vla_test",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "previous-templates-web4.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.renderer-web-main-get-previous-resource-id.state.resource_id}"
                    }
                ]
            }
        },
        "renderer-web-main-vla-commit-latest": {
            "title": "Commit resources to \"renderer_main_vla_test\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-web-main-vla-commit-previous"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_main_vla_test",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "latest-templates-web4.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.build.resource}"
                    }
                ]
            }
        },
        "renderer-web-main-is-dynamic-deploy": {
            "title": "Check if changes are dynamic",
            "task": "projects/renderer/release/is_dynamic_nanny_deploy",
            "needs": [
                "renderer-web-main-sas-prestable-commit-latest",
                "renderer-web-main-sas-stable-commit-latest",
                "renderer-web-main-vla-commit-latest"
            ],
            "input": {
                "config": {
                    "checks": [
                        {
                            "service_id": "renderer_main_sas_test_prestable",
                            "to": "${tasks.renderer-web-main-sas-prestable-commit-previous.snapshot_id}"
                        },
                        {
                            "service_id": "renderer_main_sas_test_stable",
                            "to": "${tasks.renderer-web-main-sas-stable-commit-previous.snapshot_id}"
                        },
                        {
                            "service_id": "renderer_main_vla_test",
                            "to": "${tasks.renderer-web-main-vla-commit-previous.snapshot_id}"
                        },
                        {
                            "service_id": "renderer_main_sas_test_prestable",
                            "from": "${tasks.renderer-web-main-sas-prestable-commit-previous.snapshot_id}",
                            "to": "${tasks.renderer-web-main-sas-prestable-commit-latest.snapshot_id}"
                        },
                        {
                            "service_id": "renderer_main_sas_test_stable",
                            "from": "${tasks.renderer-web-main-sas-stable-commit-previous.snapshot_id}",
                            "to": "${tasks.renderer-web-main-sas-stable-commit-latest.snapshot_id}"
                        },
                        {
                            "service_id": "renderer_main_vla_test",
                            "from": "${tasks.renderer-web-main-vla-commit-previous.snapshot_id}",
                            "to": "${tasks.renderer-web-main-vla-commit-latest.snapshot_id}"
                        }
                    ]
                }
            }
        },
        "renderer-web-main-prestable-lenour-commit-latest": {
            "title": "Commit lenour config to \"lenour_sas_prestable_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-commit-data-prepared"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_prestable_test",
                    "lenour_config": {
                        "Default": "LATEST"
                    }
                }
            }
        },
        "renderer-web-main-prestable-lenour-commit-previous": {
            "title": "Commit lenour config to \"lenour_sas_prestable_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-prestable-lenour-commit-latest"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_prestable_test",
                    "lenour_config": {
                        "Default": "PREVIOUS"
                    }
                }
            }
        },
        "renderer-web-main-prestable-lenour-commit-default": {
            "title": "Commit lenour config to \"lenour_sas_prestable_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-prestable-lenour-commit-previous"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_prestable_test",
                    "lenour_config": {
                        "Default": "LATEST",
                        "PrevVersion": "${tasks.renderer-web-main-get-previous-template-version.state.version}",
                        "LatestVersion": "${tasks.renderer-web-main-get-latest-template-version.state.version}"
                    }
                }
            }
        },
        "renderer-web-main-sas-lenour-commit-latest": {
            "title": "Commit lenour config to \"lenour_sas_stable_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-commit-data-prepared"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_stable_test",
                    "lenour_config": {
                        "Default": "LATEST"
                    }
                }
            }
        },
        "renderer-web-main-sas-lenour-commit-previous": {
            "title": "Commit lenour config to \"lenour_sas_stable_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-sas-lenour-commit-latest"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_stable_test",
                    "lenour_config": {
                        "Default": "PREVIOUS"
                    }
                }
            }
        },
        "renderer-web-main-sas-lenour-commit-default": {
            "title": "Commit lenour config to \"lenour_sas_stable_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-sas-lenour-commit-previous"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_stable_test",
                    "lenour_config": {
                        "Default": "LATEST",
                        "PrevVersion": "${tasks.renderer-web-main-get-previous-template-version.state.version}",
                        "LatestVersion": "${tasks.renderer-web-main-get-latest-template-version.state.version}"
                    }
                }
            }
        },
        "renderer-web-main-vla-lenour-commit-latest": {
            "title": "Commit lenour config to \"lenour_vla_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-commit-data-prepared"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_vla_test",
                    "lenour_config": {
                        "Default": "LATEST"
                    }
                }
            }
        },
        "renderer-web-main-vla-lenour-commit-previous": {
            "title": "Commit lenour config to \"lenour_vla_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-vla-lenour-commit-latest"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_vla_test",
                    "lenour_config": {
                        "Default": "PREVIOUS"
                    }
                }
            }
        },
        "renderer-web-main-vla-lenour-commit-default": {
            "title": "Commit lenour config to \"lenour_vla_test\"",
            "task": "projects/lenour/lenour_commit_config",
            "needs": [
                "renderer-web-main-vla-lenour-commit-previous"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_vla_test",
                    "lenour_config": {
                        "Default": "LATEST",
                        "PrevVersion": "${tasks.renderer-web-main-get-previous-template-version.state.version}",
                        "LatestVersion": "${tasks.renderer-web-main-get-latest-template-version.state.version}"
                    }
                }
            }
        },
        "renderer-web-main-all-committed": {
            "title": "\"web-main\" all committed",
            "task": "dummy",
            "needs": [
                "renderer-web-main-is-dynamic-deploy",
                "renderer-web-main-prestable-lenour-commit-default",
                "renderer-web-main-sas-lenour-commit-default",
                "renderer-web-main-vla-lenour-commit-default"
            ]
        },
        "renderer-web-main-prestable-lenour-switch-latest": {
            "title": "Set \"lenour_sas_prestable_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-sync-commits"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_prestable_test",
                    "snapshot_id": "${tasks.renderer-web-main-prestable-lenour-commit-latest.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-sas-lenour-switch-latest": {
            "title": "Set \"lenour_sas_stable_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-sync-commits"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_stable_test",
                    "snapshot_id": "${tasks.renderer-web-main-sas-lenour-commit-latest.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-vla-lenour-switch-latest": {
            "title": "Set \"lenour_vla_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-sync-commits"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_vla_test",
                    "snapshot_id": "${tasks.renderer-web-main-vla-lenour-commit-latest.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-lenour-latest-switched": {
            "title": "\"web-main\" lenour switched to LATEST",
            "task": "dummy",
            "needs": [
                "renderer-web-main-prestable-lenour-switch-latest",
                "renderer-web-main-sas-lenour-switch-latest",
                "renderer-web-main-vla-lenour-switch-latest"
            ]
        },
        "renderer-web-main-sas-prestable-prepare-previous": {
            "title": "Set \"renderer_main_sas_test_prestable\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-sync-commits"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_prestable",
                    "snapshot_id": "${tasks.renderer-web-main-sas-prestable-commit-previous.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-sas-stable-prepare-previous": {
            "title": "Set \"renderer_main_sas_test_stable\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-sync-commits"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_stable",
                    "snapshot_id": "${tasks.renderer-web-main-sas-stable-commit-previous.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-vla-prepare-previous": {
            "title": "Set \"renderer_main_vla_test\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-sync-commits"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_vla_test",
                    "snapshot_id": "${tasks.renderer-web-main-vla-commit-previous.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-previous-prepared": {
            "title": "\"web-main\" previous templates prepared",
            "task": "dummy",
            "needs": [
                "renderer-web-main-sas-prestable-prepare-previous",
                "renderer-web-main-sas-stable-prepare-previous",
                "renderer-web-main-vla-prepare-previous"
            ]
        },
        "renderer-web-main-acquire-lock-sas": {
            "title": "Acquire lock renderer_ci_web_sas_test(web/sas)",
            "task": "projects/canti/canti_lock",
            "needs": [
                "renderer-web-main-lenour-latest-switched",
                "renderer-web-main-previous-prepared"
            ],
            "input": {
                "config": {
                    "action_id": "renderer_ci_web_sas_test",
                    "path": "web/sas",
                    "priority": 0
                }
            }
        },
        "renderer-web-main-acquire-lock-vla": {
            "title": "Acquire lock renderer_ci_web_vla_test(web/vla)",
            "task": "projects/canti/canti_lock",
            "needs": [
                "renderer-web-main-lenour-latest-switched",
                "renderer-web-main-previous-prepared"
            ],
            "input": {
                "config": {
                    "action_id": "renderer_ci_web_vla_test",
                    "path": "web/vla",
                    "priority": 0
                }
            }
        },
        "renderer-web-main-acquire-lock-man": {
            "title": "Acquire lock renderer_ci_web_man_test(web/man)",
            "task": "projects/canti/canti_lock",
            "needs": [
                "renderer-web-main-lenour-latest-switched",
                "renderer-web-main-previous-prepared"
            ],
            "input": {
                "config": {
                    "action_id": "renderer_ci_web_man_test",
                    "path": "web/man",
                    "priority": 0
                }
            }
        },
        "renderer-web-main-sas-prestable-activate-previous": {
            "title": "Set \"renderer_main_sas_test_prestable\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-acquire-lock-sas",
                "renderer-web-main-acquire-lock-vla",
                "renderer-web-main-acquire-lock-man"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_prestable",
                    "snapshot_id": "${tasks.renderer-web-main-sas-prestable-commit-previous.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-sas-stable-activate-previous": {
            "title": "Set \"renderer_main_sas_test_stable\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-acquire-lock-sas",
                "renderer-web-main-acquire-lock-vla",
                "renderer-web-main-acquire-lock-man"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_stable",
                    "snapshot_id": "${tasks.renderer-web-main-sas-stable-commit-previous.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-vla-activate-previous": {
            "title": "Set \"renderer_main_vla_test\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-acquire-lock-sas",
                "renderer-web-main-acquire-lock-vla",
                "renderer-web-main-acquire-lock-man"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_vla_test",
                    "snapshot_id": "${tasks.renderer-web-main-vla-commit-previous.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-previous-activated": {
            "title": "\"web-main\" previous templates activated",
            "task": "dummy",
            "needs": [
                "renderer-web-main-sas-prestable-activate-previous",
                "renderer-web-main-sas-stable-activate-previous",
                "renderer-web-main-vla-activate-previous"
            ]
        },
        "renderer-web-main-prestable-lenour-switch-previous": {
            "title": "Set \"lenour_sas_prestable_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-web-main-previous-activated"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_prestable_test",
                    "snapshot_id": "${tasks.renderer-web-main-prestable-lenour-commit-previous.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-sas-lenour-switch-previous": {
            "title": "Set \"lenour_sas_stable_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-web-main-previous-activated"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_stable_test",
                    "snapshot_id": "${tasks.renderer-web-main-sas-lenour-commit-previous.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-vla-lenour-switch-previous": {
            "title": "Set \"lenour_vla_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-web-main-previous-activated"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_vla_test",
                    "snapshot_id": "${tasks.renderer-web-main-vla-lenour-commit-previous.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-lenour-previous-switched": {
            "title": "\"web-main\" lenour switched to PREVIOUS",
            "task": "dummy",
            "needs": [
                "renderer-web-main-prestable-lenour-switch-previous",
                "renderer-web-main-sas-lenour-switch-previous",
                "renderer-web-main-vla-lenour-switch-previous"
            ]
        },
        "renderer-web-main-sas-prestable-prepare-latest": {
            "title": "Set \"renderer_main_sas_test_prestable\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-previous-activated"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_prestable",
                    "snapshot_id": "${tasks.renderer-web-main-sas-prestable-commit-latest.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-sas-stable-prepare-latest": {
            "title": "Set \"renderer_main_sas_test_stable\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-previous-activated"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_stable",
                    "snapshot_id": "${tasks.renderer-web-main-sas-stable-commit-latest.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-vla-prepare-latest": {
            "title": "Set \"renderer_main_vla_test\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-previous-activated"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_vla_test",
                    "snapshot_id": "${tasks.renderer-web-main-vla-commit-latest.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-latest-prepared": {
            "title": "\"web-main\" latest templates prepared",
            "task": "dummy",
            "needs": [
                "renderer-web-main-sas-prestable-prepare-latest",
                "renderer-web-main-sas-stable-prepare-latest",
                "renderer-web-main-vla-prepare-latest"
            ]
        },
        "renderer-web-main-sas-prestable-activate-latest": {
            "title": "Set \"renderer_main_sas_test_prestable\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-lenour-previous-switched",
                "renderer-web-main-latest-prepared"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_prestable",
                    "snapshot_id": "${tasks.renderer-web-main-sas-prestable-commit-latest.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-sas-stable-activate-latest": {
            "title": "Set \"renderer_main_sas_test_stable\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-lenour-previous-switched",
                "renderer-web-main-latest-prepared"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_sas_test_stable",
                    "snapshot_id": "${tasks.renderer-web-main-sas-stable-commit-latest.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-vla-activate-latest": {
            "title": "Set \"renderer_main_vla_test\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-web-main-lenour-previous-switched",
                "renderer-web-main-latest-prepared"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_main_vla_test",
                    "snapshot_id": "${tasks.renderer-web-main-vla-commit-latest.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-web-main-latest-activated": {
            "title": "\"web-main\" latest templates activated",
            "task": "dummy",
            "needs": [
                "renderer-web-main-sas-prestable-activate-latest",
                "renderer-web-main-sas-stable-activate-latest",
                "renderer-web-main-vla-activate-latest"
            ]
        },
        "renderer-web-main-sleep-before-prestable": {
            "title": "Wait 5m",
            "task": "common/misc/sleep",
            "needs": [
                "renderer-web-main-latest-activated"
            ],
            "input": {
                "config": {
                    "sleep_time": "5m"
                }
            }
        },
        "renderer-web-main-prestable-lenour-switch-default": {
            "title": "Set \"lenour_sas_prestable_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-web-main-sleep-before-prestable"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_prestable_test",
                    "snapshot_id": "${tasks.renderer-web-main-prestable-lenour-commit-default.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-sleep-after-prestable": {
            "title": "Wait 10m",
            "task": "common/misc/sleep",
            "needs": [
                "renderer-web-main-prestable-lenour-switch-default"
            ],
            "input": {
                "config": {
                    "sleep_time": "10m"
                }
            }
        },
        "renderer-web-main-sas-lenour-switch-default": {
            "title": "Set \"lenour_sas_stable_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-web-main-sleep-after-prestable"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_sas_stable_test",
                    "snapshot_id": "${tasks.renderer-web-main-sas-lenour-commit-default.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-vla-lenour-switch-default": {
            "title": "Set \"lenour_vla_test\" to \"ACTIVE\"",
            "task": "projects/lenour/lenour_set_snapshot_state",
            "needs": [
                "renderer-web-main-sleep-after-prestable"
            ],
            "input": {
                "config": {
                    "service_id": "lenour_vla_test",
                    "snapshot_id": "${tasks.renderer-web-main-vla-lenour-commit-default.snapshot_id}",
                    "target_state": "ACTIVE"
                }
            }
        },
        "renderer-web-main-lenour-default-switched": {
            "title": "\"web-main\" lenour switched to DEFAULT",
            "task": "dummy",
            "needs": [
                "renderer-web-main-sas-lenour-switch-default",
                "renderer-web-main-vla-lenour-switch-default"
            ]
        },
        "renderer-web-main-all-activated": {
            "title": "\"web-main\" all activated",
            "task": "dummy",
            "needs": [
                "renderer-web-main-lenour-default-switched"
            ]
        },
        "renderer-web-main-release-lock-sas": {
            "title": "Release lock renderer_ci_web_sas_test",
            "task": "projects/canti/canti_unlock",
            "needs": [
                "renderer-web-main-all-activated"
            ],
            "input": {
                "config": {
                    "action_id": "renderer_ci_web_sas_test"
                }
            }
        },
        "renderer-web-main-release-lock-vla": {
            "title": "Release lock renderer_ci_web_vla_test",
            "task": "projects/canti/canti_unlock",
            "needs": [
                "renderer-web-main-all-activated"
            ],
            "input": {
                "config": {
                    "action_id": "renderer_ci_web_vla_test"
                }
            }
        },
        "renderer-web-main-release-lock-man": {
            "title": "Release lock renderer_ci_web_man_test",
            "task": "projects/canti/canti_unlock",
            "needs": [
                "renderer-web-main-all-activated"
            ],
            "input": {
                "config": {
                    "action_id": "renderer_ci_web_man_test"
                }
            }
        },
        "renderer-web-main-release-templates-lock-web": {
            "title": "Release lock renderer_ci_web_templates_test",
            "task": "projects/canti/canti_unlock",
            "needs": [
                "renderer-web-main-release-lock-sas",
                "renderer-web-main-release-lock-vla",
                "renderer-web-main-release-lock-man"
            ],
            "input": {
                "config": {
                    "action_id": "renderer_ci_web_templates_test"
                }
            }
        },
        "renderer-web-main-done": {
            "title": "\"web-main\" done",
            "task": "dummy",
            "needs": [
                "renderer-web-main-release-templates-lock-web"
            ]
        },
        "renderer-lowload-init": {
            "title": "Init \"lowload\"",
            "task": "dummy",
            "needs": []
        },
        "renderer-lowload-sas-prestable-commit": {
            "title": "Commit resources to \"renderer_sas_test_prestable\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-lowload-init"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_sas_test_prestable",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_LOWLOAD_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "templates-web4-lowload.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.build.resource}"
                    }
                ]
            }
        },
        "renderer-lowload-sas-stable-commit": {
            "title": "Commit resources to \"renderer_sas_test_stable\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-lowload-init"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_sas_test_stable",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_LOWLOAD_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "templates-web4-lowload.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.build.resource}"
                    }
                ]
            }
        },
        "renderer-lowload-vla-commit": {
            "title": "Commit resources to \"renderer_vla_test\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-lowload-init"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_vla_test",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_LOWLOAD_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "templates-web4-lowload.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.build.resource}"
                    }
                ]
            }
        },
        "renderer-lowload-man-commit": {
            "title": "Commit resources to \"renderer_man_test\"",
            "task": "common/nanny/update_service",
            "needs": [
                "renderer-lowload-init"
            ],
            "input": {
                "config": {
                    "target_status": "COMMITTED",
                    "service_id": "renderer_man_test",
                    "release_type": "stable",
                    "patches": [
                        {
                            "sandbox": {
                                "resource_type": "WEB_LOWLOAD_MICRO_PACKAGE",
                                "resource": {
                                    "local_path": "templates-web4-lowload.tar.gz"
                                }
                            }
                        }
                    ]
                },
                "sandbox_resources": [
                    {
                        "id": "${tasks.build.resource}"
                    }
                ]
            }
        },
        "renderer-lowload-committed": {
            "title": "\"lowload\" committed",
            "task": "dummy",
            "needs": [
                "renderer-lowload-sas-prestable-commit",
                "renderer-lowload-sas-stable-commit",
                "renderer-lowload-vla-commit",
                "renderer-lowload-man-commit"
            ]
        },
        "renderer-lowload-is-dynamic-deploy": {
            "title": "Check if changes are dynamic",
            "task": "projects/renderer/release/is_dynamic_nanny_deploy",
            "needs": [
                "renderer-sync-commits"
            ],
            "input": {
                "config": {
                    "checks": [
                        {
                            "service_id": "renderer_sas_test_prestable",
                            "to": "${tasks.renderer-lowload-sas-prestable-commit.snapshot_id}"
                        },
                        {
                            "service_id": "renderer_sas_test_stable",
                            "to": "${tasks.renderer-lowload-sas-stable-commit.snapshot_id}"
                        },
                        {
                            "service_id": "renderer_vla_test",
                            "to": "${tasks.renderer-lowload-vla-commit.snapshot_id}"
                        },
                        {
                            "service_id": "renderer_man_test",
                            "to": "${tasks.renderer-lowload-man-commit.snapshot_id}"
                        }
                    ]
                }
            }
        },
        "renderer-lowload-sas-prestable-prepare": {
            "title": "Set \"renderer_sas_test_prestable\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-lowload-is-dynamic-deploy"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_sas_test_prestable",
                    "snapshot_id": "${tasks.renderer-lowload-sas-prestable-commit.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-lowload-sas-stable-prepare": {
            "title": "Set \"renderer_sas_test_stable\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-lowload-is-dynamic-deploy"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_sas_test_stable",
                    "snapshot_id": "${tasks.renderer-lowload-sas-stable-commit.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-lowload-vla-prepare": {
            "title": "Set \"renderer_vla_test\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-lowload-is-dynamic-deploy"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_vla_test",
                    "snapshot_id": "${tasks.renderer-lowload-vla-commit.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-lowload-man-prepare": {
            "title": "Set \"renderer_man_test\" to \"PREPARED\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-lowload-is-dynamic-deploy"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_man_test",
                    "snapshot_id": "${tasks.renderer-lowload-man-commit.snapshot_id}",
                    "target_status": "PREPARED",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-lowload-prepared": {
            "title": "\"lowload\" prepared",
            "task": "dummy",
            "needs": [
                "renderer-lowload-sas-prestable-prepare",
                "renderer-lowload-sas-stable-prepare",
                "renderer-lowload-vla-prepare",
                "renderer-lowload-man-prepare"
            ]
        },
        "renderer-lowload-manual-lock-sas": {
            "title": "Deploy to sas",
            "task": "dummy",
            "needs": [
                "renderer-lowload-prepared"
            ],
            "manual": {
                "enabled": true,
                "prompt": "Deploy to sas?"
            }
        },
        "renderer-lowload-sas-prestable-activate": {
            "title": "Set \"renderer_sas_test_prestable\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-lowload-manual-lock-sas"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_sas_test_prestable",
                    "snapshot_id": "${tasks.renderer-lowload-sas-prestable-commit.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-lowload-sas-stable-activate": {
            "title": "Set \"renderer_sas_test_stable\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-lowload-manual-lock-sas"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_sas_test_stable",
                    "snapshot_id": "${tasks.renderer-lowload-sas-stable-commit.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-lowload-manual-lock-rest": {
            "title": "Deploy to vla, man",
            "task": "dummy",
            "needs": [
                "renderer-lowload-sas-prestable-activate",
                "renderer-lowload-sas-stable-activate"
            ],
            "manual": {
                "enabled": true,
                "prompt": "Deploy to vla, man?"
            }
        },
        "renderer-lowload-vla-activate": {
            "title": "Set \"renderer_vla_test\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-lowload-manual-lock-rest"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_vla_test",
                    "snapshot_id": "${tasks.renderer-lowload-vla-commit.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-lowload-man-activate": {
            "title": "Set \"renderer_man_test\" to \"ACTIVE\"",
            "task": "common/nanny/set_snapshot_state",
            "needs": [
                "renderer-lowload-manual-lock-rest"
            ],
            "input": {
                "config": {
                    "service_id": "renderer_man_test",
                    "snapshot_id": "${tasks.renderer-lowload-man-commit.snapshot_id}",
                    "target_status": "ACTIVE",
                    "prepare_recipe": "dynamic resource preparation",
                    "activate_recipe": "dynamic resource activation"
                }
            }
        },
        "renderer-lowload-activated": {
            "title": "\"lowload\" activated",
            "task": "dummy",
            "needs": [
                "renderer-lowload-vla-activate",
                "renderer-lowload-man-activate"
            ]
        },
        "renderer-lowload-done": {
            "title": "\"lowload\" done",
            "task": "dummy",
            "needs": [
                "renderer-lowload-activated"
            ]
        },
        "renderer-sync-commits": {
            "title": "Synchronize clusters commits",
            "task": "dummy",
            "needs": [
                "renderer-web-main-all-committed",
                "renderer-lowload-committed"
            ]
        },
        "renderer-sync-done": {
            "title": "Synchronize clusters done",
            "task": "dummy",
            "needs": [
                "renderer-lowload-done",
                "renderer-web-main-done"
            ]
        }
    }
}
```
</p>
</details>
