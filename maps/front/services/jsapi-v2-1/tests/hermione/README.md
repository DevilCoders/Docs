## Functional autotests

### How to run autotests locally

- MacOS: you must have `realpath` (`brew install coreutils`).
- You must logged in at least once on front-jsapi-dev.sas.yp-c.yandex.net via ssh.
- Set key-authentication.
- Run `make func-test-local`. Then new api will build and test files will be uploaded to the test host.

### How to update screenshot in failed test

- run `make func-test-update`
- click "accept" button (be sure that screenshot is valid)
- additionally, you can click "retry" button to try separate test
