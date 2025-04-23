# task-processor-lib
Библиотека для упрощения работы с таск процессором

## Компоненты
### pytest_plugin
Мок/плагин для тестов, предоставляет фикстуру `task_processor` имеющую следующие методы:
* `add_provider` - добавить и разегистрировать нового провайдера в моке
* `add_cube` - добавить и зарегистрировать новый кубик для определённого провайдера
* `add_recipe` - добавить и зарегистрировать новый рецепт для определённого провайдера
* `load_recipe` - загрузить рецепт из сырых данных (аналогично структуре создания/редактирования рецепта через апи таск процессора)
* `start_job` - запустить новую джобу для определённого рецепта
* `step` - выполнить очередную таску у запущенной джобы

Также есть вспомогательные фикстуры:
* `_default_tp_init_params` - возвращает дефолтные параметры для инициализации мока

Пример использования мока в тестах:
```(python)
# conftest.py

@pytest.fixture
def clown_cube_caller(mockserver):
    async def _do_it(cube, request_data):
        return mockserver.make_response(
            json={**request_data, 'status': 'success'},
        )

    return _do_it


@pytest.fixture
async def _default_tp_init_params(
        get_all_cubes, raw_call_cube, clown_cube_caller,
):
    clown = tp_plugin.Provider(
        name='clownductor', id=1, cube_caller=clown_cube_caller,
    )

    async def self_cube_caller(cube, request_data):
        return await raw_call_cube(name=cube.name, **request_data)

    provider = tp_plugin.Provider(
        name='clowny-balancer', id=34, cube_caller=self_cube_caller,
    )
    return {
        'providers': [clown, provider],
        'cubes': [
            *(
                tp_plugin.Cube(provider=provider, **x)
                for x in (await get_all_cubes())['cubes']
            ),
            tp_plugin.Cube(
                provider=clown,
                name='WaitPodsAllocateEnd',
                needed_parameters=['sas_pods', 'vla_pods', 'man_pods'],
                optional_parameters=[],
                output_parameters=[],
            ),
        ],
        'recipes': [],
    }


# test_recipe.py

async def test_recipe(load_yaml, task_processor):
    recipe = task_processor.load_recipe(
        load_yaml('BalancerReallocateAllPods.yaml')['data'],
    )
    job = await recipe.start_job(job_vars={'awacs_namespace_id': 'ns1'})

    while not job.status.is_terminated:
        task = await job.step()
        assert task.status.is_success if task else job.status.is_success

    assert job.job_vars == {
        'awacs_namespace_id': 'ns1',
        'balancer_service_man': 'some-long-name_man',
        'balancer_service_sas': '',
        'balancer_service_vla': '',
        'man_pod_ids': ['pod-1'],
        'sas_pod_ids': ['pod-1'],
        'vla_pod_ids': ['pod-1'],
    }
```

#### TODO:
* удобная обвязка для "мета" кубиков
