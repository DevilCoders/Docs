# Storybook

Для документирования компонентов используется библиотека [Storybook](https://storybook.js.org/).

## Использование

Документирование компонента описано [тут](https://storybook.js.org/docs/react/writing-stories/introduction).

Для выборочной сборки (существенно влияет на скорость) можно воспользоваться переменной окружения `STORYBOOK_BUILD_TARGET`

Запуск storybook для компонента Button

```
STORYBOOK_BUILD_TARGET='components/Button/Button' npm run storybook
```

Запуск storybook для проекта Avia

```
STORYBOOK_BUILD_TARGET='projects/avia/**/*' npm run storybook
```

## Доступ к dev машине

Для доступа к storybook на dev машине, нужно расширить конфиг nginx, заменить %user% на свой логин:

```
server {
    listen [::]:443 ssl;

    ssl_certificate /home/%user%/certs/dev.pem;
    ssl_certificate_key /home/%user%/certs/dev.pem;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers AES128-SHA:AES256-SHA:RC4-SHA:DES-CBC3-SHA:RC4-MD5;
    ssl_session_cache shared:SSL:128m;
    ssl_session_timeout 28h;

    server_name storybook.%user%.ui.yandex.ru;

    location / {
       proxy_pass http://127.0.0.1:6060;
    }
}
```

## Стенд

Для каждого стенда на ферме публикуется статика сгенерированная **storybook**.
Чтобы открыть storybook необходиме в url стенда добавить префикс styleguide\_ (Например: https://styleguide_ya-travel_dev.travel.farm.yandex.ru) или storybook\_ (Например: https://storybook_ya-travel_dev.travel.farm.yandex.ru).
