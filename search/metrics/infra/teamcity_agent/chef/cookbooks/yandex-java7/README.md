Description
===========

This cookbook installs a yandex-flavored Oracle Java JDK.

**IMPORTANT NOTE**

This cookbook relies on dist.yandex.ru and should be used only in
yandex network.

Requirements
============

Chef 11.6.0 and higher.

## Platform

* Ubuntu 12.04

Attributes
==========

* `node[:java][:yandex][:package]` - installed package name
 (`yandex-jdk7`, by default)
* `node[:java][:yandex][:version]` - installed package version
 (`7.45-tzdata2013d`, by default)

Recipes
=======

## default

Include the default recipe in a run list, to get `java`.

Usage
=====

Simply include the `java` recipe where ever you would like Java installed.

    name "java"
    description "Install Java"
    run_list(
      "recipe[yandex-java7]"
    )


Development
===========

This cookbook uses
[test-kitchen](https://github.com/opscode/test-kitchen) and [ServerSpec](http://serverspec.org) for
integration tests and [ChefSpec/RSpec](https://github.com/acrmp/chefspec) for unit tests.
Pull requests should pass existing tests in `spec` and `test/integration/default/serverspec`.

To run code quality checks and tests simply fire `rake all`.

License and Author
==================

* Author: Gleb M Borisov (<bgleb@yandex-team.ru>)

Copyright: 2014, Yandex, LLC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.