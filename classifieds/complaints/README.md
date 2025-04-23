Complaints
================

#### Structure
This project contains following modules:
  * `complaints-core`, `complaints-api`, `complaints-scheduler` - base modules for core, api and tasks
  * `complaints-*-core` - library models related to services, not supposed to be published anywhere
  * `complaints-*-api` - runnable modules, packed into Debian package and accessible via RESTful API; depends on `complaints-core`
  * `complaints-*-scheduler`  - runnable modules, packed into Debian package and performing a row of periodical tasks;

#### Build commands
  * Clean

    `mvn clean --projects {module-name} --also-make`
  * Compile

    `mvn compile --projects {module-name} --also-make`
  * Test

    `mvn test --projects {module-name} --also-make`
  * Deploy to development

    `mvn install --projects {module-name} --also-make -P development-deploy`

    There is `upload.properties` file must be placed in `complaints/assembly` directory.
    It must contain `ssh.username` and `ssh.host` properties. Example of `upload.properties`:

    ```
    ssh.username=dimas
    ssh.host=dev23i.vs.os.yandex.net
    ```

###Integration with IntelliJ IDEA
  * copy run configurations from ./idea_build_configurations to
    ".idea/runConfigurations"
  * maven run configuration will be available in
    Maven Projects (Panel) -> moderation -> Run Configurations

To turn on scalastyle: copy `scalastyle_config.xml` to `.idea`

###Development
[TEAMCITY](https://t.vertis.yandex-team.ru/project/Verticals_Moderation_ComplaintsArc)

[JENKINS](https://j.vertis.yandex-team.ru/job/Deploys/job/Complaints/job/testing/)
