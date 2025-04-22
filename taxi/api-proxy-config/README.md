# API Gateway Configs

## Pre-git history
- Stable: [history-stable branch](https://a.yandex-team.ru/arc_vcs/?rev=external%2Fgithub%2Ftaxi%2Fapi-proxy-config%2Fhistory-stable)
- Testing: [history-testing branch](https://a.yandex-team.ru/arc_vcs/?rev=external%2Fgithub%2Ftaxi%2Fapi-proxy-config%2Fhistory-testing)

## Pre Arcadia history
The repository has been migrated from GitHub to Arcadia at https://st.yandex-team.ru/TAXIORDER-2580. However, pull requests and other GitHub-related metadata is not available at Arcadia.
So, we have restored read-only replica at GitLab: https://gitlab.yandex-team.ru/taxi/api-proxy-config. You can use it to discover historical pull-requests.


## Team City builds:
- Testing: (`develop` + `deploy: testing` PR's) https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Tools_TaxiApiProxyConfig_Customs_CustomTesting
- Production: (`develop`) https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Tools_TaxiApiProxyConfig_Releases_Release

## Project structure:
`clusters.yaml`: alias mapping from api-proxy runtime tvm service name to its configs

`{cluster}/endpoints/{endpoint_id}` -- path to endpoint's code for cpecific cluster
  - `endpoint.yaml` general endpoint meta info
  - `control.yaml` just for historical purposes, operative state
  - `get.yaml`, `post.yaml`, `put.yaml`, `patch.yaml`, `delete.yaml` AGL code for method handlers
  - `tests/{test_name}.yaml` built-in [api-proxy test](https://wiki.yandex-team.ru/taxi/backend/architecture/apiproxy/manual2/#avtotestydljaokonechnyxtochek)

#### endpoint.yaml
- `path`: string. Endoint url. Supports regular expressions
- `summary`: string, Description
- `dev_team`: string, Your team name from [DEV_TEAMS](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/DEV_TEAMS?name=dev_teams) config. Will be used by to track dynamic permissions and juggler alerts.
- `duty_abc`: string, Responsible duty team id in [ABC](https://abc.yandex-team.ru/).

Optional:
- `clone-from`, `clone-subscribers`: endpoint clonning options, provided both for clone and original.
- `dorblu`: Dorblu generator modifications to be injected.

##### Clonning (defined endpoint.yaml)

Endpoints can be cloned with template modifications. This can be used to resolve API conflicts in evolving code when some alterations have to be injected (for experimental or security purposes).

Clonning endpoints:
```(yaml)
# Defined for clone instance
clone-from:
    cluster: <src-cluster>
    id: <src-id>
    overrides:
        resources:
          - src: <orig-resource>
            dst: <replacement-resource>
```

```(yaml)
# Defined for original instance
# all clones have to be listed there
clone-subscribers:
  - cluster: <sub-cluster>  
    id: <sub-id>
```

#### get, post, put, patch, delete handlers
See [the wiki on endpoint format](https://wiki.yandex-team.ru/taxi/backend/architecture/apiproxy/manual2/#upravlenieruchkamiapi-proxyokonechnymitochkami)

#### tests/{test_name}.yaml
See [the wiki on test format](https://wiki.yandex-team.ru/taxi/backend/architecture/apiproxy/manual2/#avtotestydljaokonechnyxtochek)

Example endoint: https://a.yandex-team.ru/arc_vcs/taxi/api-proxy-config/example/endpoints/endpoint-example

# Workflow
- make changes in your feature branch
  ```bash
  $ arc pull trunk && arc checkout trunk
  $ arc checkout -b feat-totw-cool-feature
  ... make changes
  ```
- test it
  ```bash
  $ make test-new-testing
  ```
- stage changes, commit, push, create PR to to trunk
  ```bash
  $ arc push --set-upstream {remote-branch-for-pull-request}
  $ arc pr create
  ... and dont't forget your ticket (Relates: TAXIBACKEND-42)
  ```

## Testing new changes:
Make a changes locally. Run tests on api-proxy-manager testing cluster
```bash
# runs all local uncommited changes
$ make test-new-testing
# runs test for one endpoint
$ make test-testing-{cluster}--{endpoint_id}
```

## Deploy to testing
- label your PR with `deploy: testing`
- Start a [Custom (testing) build](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Tools_TaxiApiProxyConfig_CustomTesting) selecting your endpoint as a branch.
- If the branch does not exist, follow [**Creating a new endpoint** section](https://a.yandex-team.ru/arc_vcs/taxi/api-proxy-config#creating-a-new-endpoint) to create `masters/{cluster}/{endpoint_id}` branch via [script](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts/c1d7ddb95cb74d80846c1cbf44d80496)
- Continue at https://tariff-editor.taxi.tst.yandex-team.ru/control-api-proxy/endpoints (or click at TC successfull build link), click to `Prepare a Release` to make a draft

**Warning** If your endpoint in `history-testing` enviroment differs from `history-stable`, you should create PR's that cover that difference or release the changes to the stable.

## Pass the Code Review
We require that **all** endpoint code owners approve your PR.

If your are creating new endpoint, ensure to set proper owners in [.github/CODEOWNERS](https://a.yandex-team.ru/arc_vcs/taxi/api-proxy-config#creating-a-new-endpoint/.github/CODEOWNERS). Create github groups for your team and claim ownership.

**TODO: declate owners in ya.make**

Several endpoints (that rely to api-proxy-critical cluster) are reviewed by product-infra team. We are responsible for production alerts, so, we review critical endpoints rigorously.

## Alerts

Don't forget [to subscribe to production alerts](https://wiki.yandex-team.ru/taxi/backend/architecture/apiproxy/manual2/#monitoringi) for your endpoints! Api-proxy will notify you if something goes wrong.

## Graphs
Endpoint graphs are based on dorblu. Its configs can generated by script
```
$ BUILD_DIR=/path/to/infra-cfg-graphs make generate-dorblu
``` 
New configs are generated and pushed to infra-cfg-graphs when `develop` branch updates.

Dorblu configs can be customized at `{cluster}/service.yaml` and at endpoint's `endpoint.yaml`.

See `dorblu` in [SERVICE_CONFIG_SCHEMA](https://a.yandex-team.ru/arc_vcs/taxi/api-proxy-config/scripts/clusters.py) and [ENDPOINT_META_SCHEMA](https://a.yandex-team.ru/arc_vcs/taxi/api-proxy-config/scripts/build_endpoint_def.py) for details.

## Deploy to stable
- Start a [Release](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Tools_TaxiApiProxyConfig_Release) build selecting your endpoint as a branch
- Continue at https://tariff-editor.taxi.yandex-team.ru/control-api-proxy/endpoints (or click at TC successfull build link), click to `Prepare a Release` to make a draft

## Creating a new endpoint
1. Choose `cluster` folder, where endpoint will be. Find your cluster's folder name in [`clusters.yaml`](https://a.yandex-team.ru/arc_vcs/taxi/api-proxy-config/clusters.yaml) if your doubt. Create `{cluster}/endpoints/{endpoint_id}` folder and follow code structure described above or run a [script](scripts/generate_endpoint.py) to proxy handler fully, specifying params:  
    - `cluster` -- path to `{cluster}/endpoints` folder, where endpoint directory will be created
    - `endpoint-name` -- name of the endpoint
    - `path` -- endpoint's path
    - `dev-team` -- endpoint's dev-team
    - `duty-abc` -- endpoint's duty team id
    - `resource` -- resource that will be proxyed
    - `method` -- type of request
    - `resource-id` -- resource-id in endpoint code (optional, by default `main-source`)
    - `allow-unauthorized` -- if true, `allow-unauthorized: true` will be added (optional, by default `false`)

2. Create pull request. CI automatically creates all new endpoint master branches for Teamcity builds.
3. Start `Release` or `Custom(testing)` build in TeamCity (but we strongly recommend to deploy to testing first).
4. New endpoint will appear in admin UI in **disabled** state.

## News
https://clubs.at.yandex-team.ru/taxi-productinfra-news/23
