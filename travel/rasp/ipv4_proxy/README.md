# ipv4-proxy
Прокси с ipv4-адресами из фиксированных подсетей для хождения к партнерам

## Deployment
После мержа Testenv собирает образ, наблюдаем здесь:
```http
https://beta-testenv.yandex-team.ru/project/rasp_tests/job/RASP_BUILD_DOCKER_IMAGE_IPV4_PROXY/history?limit=20
```
Конфиг джобы здесь:
```http
https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/rasp/BuildDockerImages.yaml
```

В Deploy выбираем нужный образ. Если вдруг его в выпадающем списке нет, то прописываем Repository руками и он подтянется
```http
https://qloud-ext.yandex-team.ru/projects/rasp/ipv4-proxy
```
