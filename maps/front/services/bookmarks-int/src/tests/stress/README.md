# Stress tests

## Generating ammo

1. Build the app:

    ```sh
    make build
    ```

2. Generate ammo:

    ```sh
    make gen-ammo
    ```

3. Load ammo to `MDS`:

    ```sh
    curl https://lunapark.yandex-team.ru/api/addammo.json -F'login=<your_login>' -F'dsc=<description>' -F'file=@<path_to_ammo>'
    ```

   Then update `phantom.ammofile` in `.configs/stress/*.yaml` configuration to URL from
   response.

## Deploy and fire

1. Deploy stress:

    ```sh
    npx qtools release stress --force
    ```

2. Start shooting:

    ```sh
    npx qtools fire -c .configs/stress/sync_shared_lists.yaml
    ```

3. Don't forget to undeploy stress environment after tests:

   ```sh
   make test-stress-clean
   ```
