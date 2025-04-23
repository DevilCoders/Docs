Чтобы запустить локально:
-

- Перейти в директорию проекта:
  ```bash
  cd ${ARCADIA_ROOT}/noc/macros
  ```

- Поднять компоуз:
  ```bash
  docker-compose build --no-cache && docker-compose up -d
  ```

- После этого можно подключиться напрямую к БД:
  ```bash
  psql postgres://macros:password@localhost:5432/macros
  ```

- Дальше необходимо заимпортить макросы из CVS и RT:

  ```bash
  ya make --add-result=go --no-yt-store && ./cmd/import/import --config=./etc/macros/macros-default.yaml
  ```

- Теперь можем поднять сервер:

  ```bash
  ya make --add-result=go --no-yt-store && ./cmd/macros/macros --config=./etc/macros/macros-default.yaml
  ```

  - HTTP будет запущен на ```8080``` порту
  - GRPC будет запущен на ```12345``` порту
  - Список ручек можно посмотреть в ```./macrospb/service.proto``` в ```service Macros```


- И UI:
  ```bash
  cd ./ui && yarn start
  ```
