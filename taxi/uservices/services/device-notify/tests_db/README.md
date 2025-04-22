# device-notify manual tests
These tests are not intended for automatic execution in tests because of
large amount of rows processed here.
Purpose: speed test of pgaas schema.

## How to run

#### Build the service

#### Prepare environment
~~~
./build/testsuite/taxi-env start
~~~
#### Log output to file
Ensure that `build/services/device-notify/testsuite/configs/service.yaml`
is configured to use a file instead of `@stderr`

~~~
logging:
  loggers:
    default:
      file_path: '/taxi/uservices/.logs/server.log'
      level: debug
~~~

#### Run the tests
~~~
./build/testsuite/runtests --no-env -vvsx services/device-notify/tests_db/test_fallback_cleaner_many.py
./build/testsuite/runtests --no-env -vvsx services/device-notify/tests_db/test_inactive_users_many.py
~~~

#### Stop environment
~~~
./build/testsuite/taxi-env stop
~~~
