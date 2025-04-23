# dependency_converter.py
The script converts pom.xml dependency format into the Bazel one.

**Requires Python 3.8+.**

Usage:
```commandline
./vs-quality/scripts/maven-migration/dependency_converter.py <module-root> [<workspace>]'
```
where:
* module-root (**required**) - path to a **child** Maven module (e.g. **vs-quality/hobo/hobo-dao**)
* workspace (optional) - path to a workspace

The result is the list of module dependencies in Bazel BUILD file suitable format.
If there is no dependency in WORKSPACE - there will be a comment about this with dependency format allowed in WORKSPACE file

Works like a charm with the classic flat Maven project structure
when a child module doesn't have other children so **do not** treat this like a universal solution.

## Example
```commandline
./vs-quality/scripts/maven-migration/dependency_converter.py vs-quality/hobo/hobo-api
```
output:
```commandline
"@maven//:ru_yandex_vertis_hobo_server" # ru.yandex.vertis:hobo-server:1.0-SNAPSHOT
"@maven//:ru_yandex_vertis_hobo_test_util" # ru.yandex.vertis:hobo-test-util:1.0-SNAPSHOT
"@maven//:ru_yandex_vertis_akka_http_util_2_13"
"@maven//:com_typesafe_akka_akka_slf4j_2_13"
"@maven//:com_typesafe_akka_akka_http_testkit_2_13"
"@maven//:com_typesafe_akka_akka_testkit_2_13"
"@maven//:org_webjars_jquery" # org.webjars:jquery:3.3.1
"@maven//:org_webjars_bootstrap" # org.webjars:bootstrap:4.1.3
"@maven//:org_webjars_bowergithub_gitbrent_bootstrap4_toggle" # org.webjars.bowergithub.gitbrent:bootstrap4-toggle:3.4.0
"@maven//:com_softwaremill_sttp_client3_async_http_client_backend_future_2_13"
```
