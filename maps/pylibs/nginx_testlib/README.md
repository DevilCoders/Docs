# Maps NGINX Configuration Testing Library

[TOC]

This tiny library may be used to test **NGINX** configuration.

## Usage

See usage examples:

* [/arc/trunk/arcadia/maps/mobile/server/proxy/config/mapkit2/tests](Mobile Proxy mapkit2 tests)

In your tests you have to provide pathes to different configuration directories and files:

```python

class ServiceTestBase(NginxTestBase):
    def setUp(self):
        super(ServiceTestBase, self).setUp()

        self.set_config(
            nginx_path=os.path.join(yatest.common.binary_path('nginx/bin-noperl'), 'nginx'),
            config_dir=yatest.common.source_path('maps/pylibs/nginx_testlib/config'),
            environments_dir=yatest.common.source_path('maps/mobile/server/proxy/config/common/environments'),
            executor=yatest.common.execute)

```

* *nginx_path* --- path to nginx building project (just set to `nginx/bin-noperl`)
* *config_dir* --- path to directory, containing default nginx testing configuration files (`maps/pylibs/nginx_testlib/config`)
* *environments* --- path to file with pre-set nginx environment variables (you must create your own file for your tests)
* *executor* --- function to execute binaries, set it to `yatest.common.execute`

You also have to set a path to locations configuration files, e.g.:

```python
self._locations_path = 'maps/mobile/server/proxy/config/mapkit2/locations'
```

You may also use some helper functions to write your **NGINX** configuration tests:

* `add_require_path` --- add directory containing lua scripts to require path
* `replace_in_config` --- replace all matches in configuration files by some string
* `add_package` - execute `require "package-name"` during lua initialization
* `add_file_template` --- copy template file to work dir and replace parameters with given values
* `add_locations_from_file` --- add locations to be tested from a particular locations file
* `add_upstream`, `add_dummy_upstreams` --- create a mock upstream to check **NGINX** redirections
* `add_variable` --- add **NGINX** configuration variable
