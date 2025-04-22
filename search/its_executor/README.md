# ITS EXECUTOR

Top level API to interact with [ITS](https://wiki.yandex-team.ru/runtime-cloud/nanny/its/)

1. Create your recipe
    ```yaml
    operations:
      - balancer_id: '_test/b/its-ui-test/cplb_balancer_load_switch/'
        operations:
          - section_id: 'kek'
            operations:
            - location_id: 'VLA'
              param:
                name: 'vla'
                default_value: 0
              change: 'CLOSE'
            - location_id: ['MAN', 'SAS']
              param:
                name: 'man_sas'
                default_value: 10
              change: 'INCREASE_CURRENT'
            - location_id: 'VLA'
              param:
                name: 'vlainc'
                default_value: 50
              change: 'SET_CURRENT'
    ```
2. Execute it
    ```
    its_executor my_recipe.yaml
    ```
3. Change params?
    ```
    its_executor my_recipe.yaml --params='man_sas=13;vlainc=35'
    ```
4. Want to test recipe?
    ```
    its_executor my_recipe.yaml --dry
    ```
5. See more
    ```
    its_executor --help
    ```
