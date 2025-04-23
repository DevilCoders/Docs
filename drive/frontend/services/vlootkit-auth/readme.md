## Env Variables

`DM_VERSION` - code version
`DM_PORT` - server port number

`DM_DOMAIN` - server domain
`DM_SECRET` - secret key for crypto

`DM_AWS_USER_POOL_ID` - AWS Cognito user pool id
`DM_AWS_CLIENT_ID` - AWS Cognito client id
`DM_AWS_REGION` - AWS Cognito region name

## Vlootkit

build and deploy
`AWS_ACCESS_KEY_ID=<secret> AWS_SECRET_ACCESS_KEY=<secret> AWS_DEFAULT_REGION=eu-central-1 aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 869374968268.dkr.ecr.eu-central-1.amazonaws.com && ~/projects/arc0/arcadia/ya package drive/frontend/services/vlootkit-auth/ya-package.json --docker --docker-network host --docker-registry 869374968268.dkr.ecr.eu-central-1.amazonaws.com --docker-push`

run locally
`AWS_ACCESS_KEY_ID=<secret> AWS_SECRET_ACCESS_KEY=<secret> AWS_DEFAULT_REGION=eu-central-1 aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 869374968268.dkr.ecr.eu-central-1.amazonaws.com && docker run --rm -p 8000:80 --name vlootkit-auth-container --env-file env/dev 869374968268.dkr.ecr.eu-central-1.amazonaws.com/vlootkit/vlootkit-auth:users.next0.DRIVEMATICSDEV-399-r9637980`
