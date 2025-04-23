# @yandex-lego/storybook-deploy
В первую очередь пакет используется командой Лего для того чтобы выкладывать сторибуки, которые конфигурируются с помощью пакета `@yandex-lego/storybook-showcase`, но ничего не мешает использовать его для выкладки своего сторибука на S3. Подробнее в разделе [Как пользоваться для своих нужд](##-Как-пользоваться-для-своих-нужд).
Если вы хотите заехать на [лего сайт](https://lego.yandex-team.ru/components/lego/latest/), то переходите в раздел [Как добавить storybook своего пакета на Лего сайт](##-Как-добавить-storybook-своего-пакета-на-Лего-сайт)

## Установка
```sh
npm i @yandex-lego/storybook-deploy --save-dev
```

## Как пользоваться для своих нужд
Укажите в переменных окружения ключи от S3 бакета:
`CUSTOM_ACCESS_KEY_ID` и `CUSTOM_SECRET_ACCESS_KEY`  
по дефолту используются ключи от Лего бакета

Пример конфига для бакета frontend-test:
```
module.exports = {
    path: 'build/static/storybook',
    bucket: 'frontend-test',
    s3AccessKeyId: process.env.FRONTEND_S3_ACCESS_KEY_ID,
    s3SecretAccessKey: process.env.FRONTEND_S3_SECRET_ACCESS_KEY,
    skipVersions: true,
};
```

Поддерживаемые опции:
```
--config       - Путь до конфига
--bucket       - Название вашего бакета
--skipVersions - Отключает опцию версионирования
--path         - Директория, где хранится storybook (по умолчанию storybook)
--prefix       - Адрес конечного storybook (например story/@yandex-int/ydo/master)
```

## Удалить storybook с S3 (при закрытии ПР)
```
storybook-deploy delete
```

## Как добавить storybook своего пакета на Лего сайт

1. `npm i @yandex-lego/storybook-showcase --save-dev` Если у вас уже есть, то переходите к пункту 4
2. Выполните шаги 2 и 3 из [README пакета @yandex-lego/storybook-showcase](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/storybook-showcase/README.md)
3. Добавьте к себе в пакет скрипты про deploy:
   
```json
{
  "ci:deploy": "npm run deploy:static",
  "ci:deploy:master": "npm run deploy:static",
  "deploy:static": "storybook-showcase build && storybook-deploy"
}
```

4. На лего сайте в [файле](https://github.yandex-team.ru/serp-design/design-system/blob/master/apps/design-system-web/src/state/data/components.js) добавьте ссылку на свой сторибук и название пакета.
