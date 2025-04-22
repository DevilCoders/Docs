Backend for frontend (BFF) https://crm.yandex-team.ru

## Требования
1) node 16
1) npm 8

## Запуск
### Устанавливаем зависимости и секреты
1) npm i
1) npx make-my-env

### Устанавливаем TVM Tool и запускаем
1) npm install --global tvmtool-bin --registry=https://npm.yandex-team.ru
1) tvmtool --port 8001 --auth tvmtool-development-access-token

### Запускаем сборку
1) npm run build:watch

### Запускаем сервер
1) npm run start
1) заходим https://crm.local.yandex-team.ru
1) proxy смотрит на бекенд с https://crm-test.yandex-team.ru

## Deploy
change version in deploy.bash and run
