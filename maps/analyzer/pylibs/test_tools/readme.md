Test tools
===

### Graph & Local YT

Add to your `ya.make`:
```make
INCLUDE(${ARCADIA_ROOT}/maps/analyzer/pylibs/test_tools/test_tools.inc)
```

Optionally add `DEPENDS` to required graphs, coverage, geobase and calendar for example:
```make
DEPENDS(
    maps/data/test/calendar
    maps/data/test/geobase
    maps/data/test/geoid
    maps/data/test/graph3
    maps/data/test/trf
)
```

There're fixtures `geobase`, `coverage` and `calendar` to setup `geodata`/`tzdata`, coverage and calendar files.

Then define fixtures in `conftest.py`, using these functions:

`test_graph` — set test graph root:
  * `pkg_root` — arcadia-relative path to `PACKAGE` target with all stuff (see `maps/analyzer/toolkit/pkg` or other `pkg` targets in `maps/analyzer`)
  * `graph_version` — default graph version

`local_yt` — starts local YT:
  * `local_cypress_dir` — arcadia-relative path to directory with tables

`local_ytc` — all-in-one function, sets graph root, starts local YT and returns preconfigured `YtContext`

### Local YQL

If you additionaly want local YQL, add this:
```make
INCLUDE(${ARCADIA_ROOT}/maps/analyzer/pylibs/test_tools/local_yql.inc)
```

If you want local YQL connect to your local YT, you MUST define `yt_stuff` fixture.<br>
So, for example, if you had used `local_ytc`:
```python
@pytest.fixture()
def ytc(request):
    with test_tools.local_ytc(
        pkg_root='path/to/pkg',
        local_cypress_dir='path/to/cypress',
    ) as ctx:
        yield ctx
```
You should split it into two fixtures, one of which will be `yt_stuff`, so that local YQL will catch it:
```python
@pytest.fixture()
def yt_stuff(request):
    with test_tools.local_yt(local_cypress_dir='path/to/cypress') as stuff:  # pass local cypress dir here
        yield stuff

@pytest.fixture()
def ytc(request, yt_stuff):  # NOTE: dep on yt_stuff
    with test_tools.local_ytc(
        pkg_root='path/to/pkg',
        proxy=yt_stuff.get_server(),  # attach to local YT
    ) as ctx:
        yield ctx
```
And you're done

### Examples

See [signals_reports](/arc/trunk/arcadia/maps/analyzer/sandbox/signals_reports) for example:
  * [signals_reports/pkg](/arc/trunk/arcadia/maps/analyzer/sandbox/signals_reports/pkg) — `pkg` target to be passed as `pkg_root` arg
  * [signals_reports/tests/ya.make](/arc/trunk/arcadia/maps/analyzer/sandbox/signals_reports/tests/ya.make) — tests `ya.make`
  * [signals_reports/tests/conftest.py](/arc/trunk/arcadia/maps/analyzer/sandbox/signals_reports/tests/conftest.py) — usage of `local_ytc`
  * [signals_reports/tests/cypress](/arc/trunk/arcadia/maps/analyzer/sandbox/signals_reports/tests/cypress) — local cypress
  * [sandbox/eta_prediction/online_eta_quality/tests/conftest.py](/arc/trunk/arcadia/maps/analyzer/sandbox/eta_prediction/online_eta_quality/tests/conftest.py) — local YT + local YQL
