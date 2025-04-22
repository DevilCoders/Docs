```
   __  __                          __           __            _
  / / / /_______  _____      _____/ /_  _______/ /____  _____(_)___  ____ _
 / / / / ___/ _ \/ ___/_____/ ___/ / / / / ___/ __/ _ \/ ___/ / __ \/ __ `/
/ /_/ (__  )  __/ /  /_____/ /__/ / /_/ (__  ) /_/  __/ /  / / / / / /_/ /
\____/____/\___/_/         \___/_/\__,_/____/\__/\___/_/  /_/_/ /_/\__, /
                                                                  /____/
```

*User-clustering* is *Yandex Verticals* users clustering system, based on
[Embedded Neo4j library](https://neo4j.com/docs/java-reference/current/#tutorials-java-embedded).
ß
#### Projects wiki

https://wiki.yandex-team.ru/vertis/clustering/

#### Structure

* `user-clustering-core`    - library model, not supposed to be published anywhere
* `user-clustering-builder` - database builder
* `user-clustering-api`     - client API
* `user-clustering-tasks`   - tasks scheduler

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

  There is `upload.properties` file must be placed in `service-api/assembly` directory. It must contain `ssh.username`
  and `ssh.host` properties. Example of `upload.properties`:

  ```
  ssh.username=junkyman
  ssh.host=decrepit01.dev.machin.yandex.net
  ```

### Integration with IntelliJ IDEA

For handy running builds from IntelliJ IDEA one should create `Maven Run Configuration` for each case (`clean`
, `compile`, `test`, development deploy, etc.)

These run configurations will be available

- via `Run Configurations` panel and
- via `Maven Projects` tab: `{Project Name}` -> `Run Configurations`
