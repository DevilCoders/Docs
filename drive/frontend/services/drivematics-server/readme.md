## Env Variables

`DM_PROFILE` - ('test' | 'prod') project env
`DM_VERSION` - code version
`DM_PORT` - server port number
`DM_YDEPLOY` - logger stream format

`DM_API_TIMEOUT` - api timeout (default: 1500ms)

`DM_STARTREK_TOKEN` - startrek robot token

## Drivematics

Build Porto Layers task: https://sandbox.yandex-team.ru/task/1210581135/view
Deploy script: `./tools/release.sh`

YDeploy Testing stage: https://deploy.yandex-team.ru/stages/drivematics-testing
YDeploy Production stage: https://deploy.yandex-team.ru/stages/drivematics-production

## Vlootkit

build and deploy
`AWS_ACCESS_KEY_ID=<secret> AWS_SECRET_ACCESS_KEY=<secret> AWS_DEFAULT_REGION=eu-central-1 aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 869374968268.dkr.ecr.eu-central-1.amazonaws.com && ya package drive/frontend/services/drivematics-server/ya-package.json --docker --docker-network host --docker-registry 869374968268.dkr.ecr.eu-central-1.amazonaws.com --docker-push`

run locally
`AWS_ACCESS_KEY_ID=<secret> AWS_SECRET_ACCESS_KEY=<secret> AWS_DEFAULT_REGION=eu-central-1 aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 869374968268.dkr.ecr.eu-central-1.amazonaws.com && docker run --rm -p 8000:80 --name vlootkit-server-container --env-file env/dev 869374968268.dkr.ecr.eu-central-1.amazonaws.com/vlootkit/vlootkit-server:users.next0.DRIVEMATICSDEV-399-r9637980`
