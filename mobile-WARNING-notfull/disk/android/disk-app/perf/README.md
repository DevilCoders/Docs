## Overview

This directory contains various files needed to run performance tests
using Pulse test infrastructure. See wiki for more information about Pulse:
https://wiki.yandex-team.ru/pulse/

The tests (also called *benchmarks*) are run with
[catapulse](https://pypi.yandex-team.ru/repo/default/catapulse/) Python
library based on [catapult](https://github.com/catapult-project/catapult)
project.

## Directory structure

- `benchmarks`: this directory contains descriptions for all the tests to be run
  as performance benchmarks. Now the most useful file here is
  `benchmarks/instrumented.py`, which defines all the benchmarks that are run as
  instrumented Android tests from `ru.yandex.disk.perftests.runner.test`
  package.
- `archives`: this directory contains links to WPR archives (`*.wprgo.mds`) to
  be used for mocked HTTP responses while running benchmarks. Archives
  themselves are not checked-in and downloaded on demand before benchmarks run.
  Archive files use `*.wprgo` extension with the same base name.

## How to use
install catapulse https://wiki.yandex-team.ru/pulse/perftests/writing_perftest/#zapusk

Run command:
`python -m catapulse.run_benchmark perf run --device=[EMULATOR NAME] [TEST NAME]`

Example:
`python -m catapulse.run_benchmark perf run --device=emulator-5554 ru.yandex.disk.perftests.runner.InitialLoadTest`

Record .wprgo files:
`python -m catapulse.record_wpr perf --device=[DEVICE NAME] [TEST CLASS]`

Known flags:
`-vv` - for more logs
`--output %EMPTY_DIR_NAME%` - to save reported metrics to file