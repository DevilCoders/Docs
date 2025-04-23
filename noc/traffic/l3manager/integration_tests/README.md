L3MGR Integration Tests
---------
The package supposed to be used to run integration tests on L3MGR components and to test l3mgr to l3mgr-balancer-agent interaction

Installing
----------
Install a venv with requirements on hosts that have access to production and testing l3 api.

A Simple Example
----------------
`python -m pytest src/l3mgr_intergation_tests/test_agent`


Configuration parameters
----------------
##### global settings
-  `stage` - defines agent's environment settings, including but not limited to logging settings, env variables and testing settings.
Avaliable values - `production` `development` `test`.
Default - No defaults. Must be set in config

##### section [api]
###### section [api.test]
- `TEST_ENV_L3MGR_TOKEN` - oauth token for L3MGR test API
- `TEST_API_URL` - L3MGR test API URL

###### section [api.prod]
- `PROD_L3MGR_READONLY_TOKEN` - robot-ttmgmt-builder read only oauth token for L3MGR prod API
- `PROD_API_URL` -  - L3MGR prod API URL

Links
-----
- ###### Arc: https://a.yandex-team.ru/arc/trunk/arcadia/noc/traffic/l3mgr-integration-tests
