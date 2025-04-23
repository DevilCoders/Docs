# Functional tests

## Record mode

After preparing environment and writing test, you have to run it in record mode to prepare mocks and save reference screenshots:

To run a single test in record mode:
```bash
FTESTS_MODE=record FTESTS_MATCH=specify_test_file_name_here make ftests
```

Don't run all tests (without specifying exact `FTESTS_MATCH`) in record mode.

## Update-snapshot mode

To update test shapshot without rewriting mocks:
```bash
FTESTS_MODE=update-snapshot FTESTS_MATCH=specify_test_file_name_here make ftests
```

## Play mode

To run a single test in play mode:
```bash
FTESTS_MATCH=specify_test_file_name_here make ftests
```

To run all tests in play mode:
```bash
make ftests
```

## Stand host

By default tests are run on dev stand host (`nmaps-dev.stands.maps.yandex.{{tld}}`). To run test on another host specify it with `FTESTS_STAND_HOST` environment variable.

```bash
FTESTS_STAND_HOST=nmaps.tst.maps.yandex.{{tld}} make ftests
```

You shouldn't specify exact tld domain in `FTESTS_STAND_HOST`, `{{tld}}` part of host will be replaced with appropriate value.
