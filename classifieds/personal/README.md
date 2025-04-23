vertis-personal-api
================

### Как катить
https://t.vertis.yandex-team.ru/project/VerticalsBackend_PersonalApi
Run на docker-release

### About
[Wiki](https://wiki.yandex-team.ru/vertis/personal)

Testing: http://personal-api-int.vrts-slb.test.vertis.yandex.net
Testing with branch: http://pull-???.personal-api-int.vrts-slb.test.vertis.yandex.net

### Build commands
  * Clean

    `mvn clean --projects {module-name} --also-make`
  * Compile

    `mvn compile --projects {module-name} --also-make`
  * Test

    `mvn test --projects {module-name} --also-make`
  * Deploy to development

    `mvn install --projects {module-name} --also-make -P development-deploy`

    There is `upload.properties` file must be placed in `service-api/assembly` directory.
    It must contain `ssh.username` and `ssh.host` properties. Example of `upload.properties`:

    ```
    ssh.username=dimas
    ssh.host=dev23i.vs.os.yandex.net
    ```


### Integration with IntelliJ IDEA

To turn on scalafmt:
  1) go to `Editor | Code Style | Scala`
  2) choose `Formatter: scalafmt`
  3) choose `Reformat on file save`
  
For handy running builds from IntelliJ IDEA one should
create `Maven Run Configuration` for each case (`clean`, `compile`, `test`, development deploy, etc.)

These run configurations will be available
  - via `Run Configurations` panel and
  - via `Maven Projects` tab: `{Project Name}` -> `Run Configurations`
