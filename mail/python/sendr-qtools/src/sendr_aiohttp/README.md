# sendr_aiohttp

### apispec
Чтобы научить приложение отдавать `swagger.json`, нужно:
1. Обернуть все `web.View.{post,get,...}` декораторами `request_schema`, `response_schema`.
2. После того, как в приложение добавлены все необходимые ресурсы, вызвать `create_apispec`. Эта функция соберет инстанс
   `APISpec`. Функция `setup_swagger_route` добавит в приложение новый эндпоинт, отдающий `swagger.json`.
