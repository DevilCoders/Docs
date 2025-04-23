```
          _______  _______  _______         _______           _       _________ _______           _______  _______
|\     /|(  ____ \(  ____ \(  ____ )       (  ____ )|\     /|( (    /|\__   __/(  ____ \|\     /|(  ____ \(  ____ )
| )   ( || (    \/| (    \/| (    )|       | (    )|| )   ( ||  \  ( |   ) (   | (    \/| )   ( || (    \/| (    )|
| |   | || (_____ | (__    | (____)| _____ | (____)|| |   | ||   \ | |   | |   | (_____ | (___) || (__    | (____)|
| |   | |(_____  )|  __)   |     __)(_____)|  _____)| |   | || (\ \) |   | |   (_____  )|  ___  ||  __)   |     __)
| |   | |      ) || (      | (\ (          | (      | |   | || | \   |   | |         ) || (   ) || (      | (\ (
| (___) |/\____) || (____/\| ) \ \__       | )      | (___) || )  \  |___) (___/\____) || )   ( || (____/\| ) \ \__
(_______)\_______)(_______/|/   \__/       |/       (_______)|/    )_)\_______/\_______)|/     \|(_______/|/   \__/

```

*User-punisher* is *Yandex Verticals* users punishment tasks engine.


#### Projects wiki
https://wiki.yandex-team.ru/vertis/user-punisher/


#### Structure
  * `user-punisher-core`  - library model, not supposed to be published anywhere
  * `user-punisher-tasks` - tasks engine
  * `user-punisher-api`   - client API


#### Build commands
  * Clean

    `make clean`
  * Compile

    `make {module-name}/compile`

    `make compile` - whole project
  * Test

    `make {module-name}/test`

    `make test` - whole project
  * Deploy to development

    `make {module-name}/install`

    There is `upload.properties` file must be placed in `service-api/assembly` directory.
    It must contain `ssh.username` and `ssh.host` properties. Example of `upload.properties`:

    ```
    ssh.username=grandshaggy
    ssh.host=grandshaggy.sas.onfire.dev.yandex.net
    ```

#### Integration testing with Testcontainers
Some of the tests are depending on [Testcontainers](https://www.testcontainers.org/) – library that supports JUnit tests, providing lightweight, throwaway instances of common databases that can run in a Docker container.

In order to run them make sure that you have Docker machine installed locally.

Make sure config file `~/.docker/config.json` is there, and it contains "auths" section

```
{
  "auths" : {
    "https://registry.yandex.net" : {
    }
  },
  "credsStore" : "osxkeychain"
}
```

### Integration with IntelliJ IDEA
For handy running builds from IntelliJ IDEA one should
create `Maven Run Configuration` for each case (`clean`, `compile`, `test`, development deploy, etc.)

These run configurations will be available
  - via `Run Configurations` panel and
  - via `Maven Projects` tab: `{Project Name}` -> `Run Configurations`
