We need to validate juggler check format with check schema, which is stored in Wall-e. For this purpose Wall-e handle /v1/scheme-validators was implemented.

Our tests compare their output with expected one, and if it differs -- validates current output using scheme-validators handle.

To minimize usage of API handle, tests use Arcadia feature called "test canonization" (https://wiki.yandex-team.ru/yatool/test/#canonization). It means that reference test output is stored in VCS and every test's output is compared with reference (canonical output).
To create reference test output, run tests with `-Z --test-param canonization [--test-param url=api_url]` option. Canonization will create `<your_testing_path>/canondata` put and canonized data there.

