## secret-service client
```
make build-cli
```
Creating tokens through yandex-passport-vault api, storing them in secret-service
Get OAuth token here: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f33f3a3b3fbe4f28a870ac070d60e681
Secrets are here: https://yav.yandex-team.ru

### building for testing
Cli tool for testing secret-service works with yav-prod: https://yav.yandex-team.ru
```
make build-cli-test
./sscli-test delegate --secret-id <id> <service>
```
### push to s3
set s3 config: https://wiki.yandex-team.ru/vertis-admin/mds-s3-share/
```
make push-sscli
```