AppHost source load test
==============================================

This sandbox task uses arcadia/tools/dolbilo to send requests to your servant. The results are generated based on the output of the servant's unistat handle.

## How to use it
Your servant should be packed into an archive together with all the data/configs/etc it needs to start. The task looks for a script called ``custom`` and runs it.

## Example (tests arcadia/apphost/tools/perftest_servant)
#### Archive layout:
example_archive/
example_archive/custom
example_archive/perftest_servant
#### custom script:
```bash
#!/usr/bin/env bash
port="$1"
script_directory="$2"

echo $0 $(pwd) $port $script_directory

${script_directory}/perftest_servant -p ${port} -t dummy
```

## Notes
* Shebang is required.
* The archive can be uploaded to sandbox via the ``REMOTE_COPY_RESOURCE`` task or via ``ya upload``
* Use ``BENCHMARK_APP_HOST_DIFF2`` task to compare 2 load test results
