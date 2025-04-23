# chat-backend
API and jobs for chatting support

#### git-hooks
To enable git hooks you need to cd to `<project directory>/scripts/hooks` and run
`chmod +x setup-git-hooks.sh && ./setup-git-hooks.sh`

If you need to update hooks, just run `./setup-git-hooks.sh` after pulling changes from github.


#### test containers
If you want to reuse test containers between test runs create `.testcontainers.properties` 
file in your home directory and put `testcontainers.reuse.enable=true` flag inside

# Deploy

### shiva 
- api чатов auto.ru: https://admin.vertis.yandex-team.ru/services/chat-api-auto
- api чатов realty: https://admin.vertis.yandex-team.ru/services/chat-api-realty
- процессор чатов: https://admin.vertis.yandex-team.ru/services/chat-processor

### teamcity
- компиляция и тесты: https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_ChatBackend_ChatCompileRunTestsArcadiaShiva?mode=builds
- api чатов auto.ru: https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_ChatBackend_ChatApiAutoruDockerArcadiaShiva?mode=builds 
- api чатов realty: https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_ChatBackend_ChatApiRealtyDockerArcadiaShiva?mode=builds
- процессор чатов: https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_ChatBackend_ChatProcessorDockerArcadiaShiva?mode=builds
