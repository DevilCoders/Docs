PRO AUTO
================

Project template for:

* Scala source code
* Maven build
* Debian build
* development deploys

#### Structure

This example project contains three modules of some abstract auto-vin-decoder:

* `carfax-core` - library model, not supposed to be published anywhere
* `carfax-api`  - runnable module, may be deployed to development;
* `carfax-scheduler`  - runnable module, may be deployed to development;
* `carfax-consumers`  - runnable module, may be deployed to development;
* `carfax-tasks`  - runnable module, may be deployed to development;

#### Build commands

* Clean

  `mvn clean --projects {module-name} --also-make`
* Compile

  `mvn compile --projects {module-name} --also-make`
* Test

  `mvn test --projects {module-name} --also-make`
* Deploy to development

  `mvn install --projects {module-name} --also-make -P development-deploy`

  There is `upload.properties` file must be placed in `carfax-api/assembly` directory. It must contain `ssh.username`
  and `ssh.host` properties. Example of `upload.properties`:

  ```
  ssh.username=dimas
  ssh.host=dev23i.vs.os.yandex.net
  ```
* Code format

  `make fmt` - format code in changed files

  `make fmt-full` - reformat whole project

### Integration with IntelliJ IDEA

To turn on scalafmt support: go to `Preferences` -> `Editor` -> `Code Style` -> `Scala` and choose `scalafmt`
as `Formatter`

For handy running builds from IntelliJ IDEA one should create `Maven Run Configuration` for each case (`clean`
, `compile`, `test`, development deploy, etc.)

These run configurations will be available

- via `Run Configurations` panel and
- via `Maven Projects` tab: `{Project Name}` -> `Run Configurations`

### NB

This template is realization of vertical guidelines https://wiki.yandex-team.ru/vertis/guidelines/
But it still doesn't satisfy all requirements. Check it ;)
