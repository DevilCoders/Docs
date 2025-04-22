# realty-map-survey-frontend

https://realty.yandex.ru/survey/maps/

Базовый путь, по которому поднимается тест, при необходимости меняется в файле `client/constants/path.js` и отдельно в `.html` файлах: `client/index.html` и `client/html/*.html`.

Чтобы собрать: `make build`. Для прода: `make build-prod`.

Текущие location'ы для nginx конфига:
```
# Surveys pages and theirs assets
location ~ ^/survey/maps(/q/\d|/result)?/?$ {
    root $root/static;
    try_files /survey/maps/index${arg_w}.html /survey/maps/index.html;
}

location /survey/ {
    root $root/static;
}
```
