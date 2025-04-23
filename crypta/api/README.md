### IntelliJ IDEA

To set up this project in IDEA use:
```
ya ide idea -C . -r ~/path/to/your/idea/project
```

Should you have any problems with Protobuf-generated code or related native libraries (.so/.dll/.dylib), try building the project
with
```
ya make
```

### Environment

Get token via `https://sandbox.yandex-team.ru/oauth`, set `SANDBOX_OAUTH_TOKEN` with the value.

Get token via `https://oauth.yandex-team.ru/authorize?response_type=token&client_id=637ca17604cb4dfa90b262952c00b1e9`, set `REACTOR_TOKEN` with the value.

And run `get_environment.sh` to get the list of required environment variables to set before
running the application.
The latest `geodata.bin` will be downloaded so expect it to be done in several minutes.

Use `Run` - `Edit Configurations...` - `Environment Variables` to set them in IntelliJ IDEA.

#### Local environment

In the absence of connection to production auth services or production auth secrets you can use the following env variables to make app work:
- DISABLE_AUTH - disables incoming auth checks
- DISABLE_TVM - disables outgoing TVM checks (resources with tvm auth will be unavailable)

### Codestyle

To adopt the proper codestyle add the plugin .jar suggested by `ya ide idea` into your IntelliJ IDEA.

### CI

This package is being automatically built by TestEnv: https://testenv.yandex-team.ru/?screen=job_history&database=crypta&job_name=BUILD_CRYPTA_API_DOCKER

### Deployment

`crypta/api` is deployed using Docker images in Platform. See `docker/Dockerfile` in this directory for more details.

- Successful builds are deployed to the testing environment automatically.
- To update the production environment go to https://platform.yandex-team.ru/projects/crypta/api then choose the environment.
  `Update` the tag of docker image.

### Additional information

This is where Reactor API is used, to learn more about it see https://wiki.yandex-team.ru/nirvana/reactor/api/http
