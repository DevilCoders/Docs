### Чтобы организовать кастомизацию новой акции в тюнинге нужно

1. Загрузить на yastatic картинки для новой акции

2. Завести ключи в танкере с текстом для акции

3. Сформировать json и отдать его бекенду

для тюнинга payload_type=web_tuning

```
{
 "text_tanker": { "tanker_project": "front-ps-tuning", "tanker_key_set": "new-year-2022", "tanker_key": "promo-title" },
 "background": "https://yastatic.net/s3/disk/promo/new-year-2022/tuning/background-image.jpg",
 "illustration": "https://yastatic.net/s3/disk/promo/new-year-2022/tuning/grid-promo.png",
 "theme": "dark",
 "link": "https://360x2022.yandex?from=tuning"
 "tariffs": {"withSubtitle": true} // если нужен подзаголовок с датой окончания акции
}

```

### Как загружать картинки в s3

1. получить права на заливку в бакет disk и настроить доступ

https://github.yandex-team.ru/personal-services/frontend/tree/dev/services/disk#контейнер-для-сборки

(в `~/.aws/credentials` должны быть прописаны aws_access_key_id и aws_secret_access_key для доступа)

проверить к каким бакетам настроен доступ

`aws --endpoint-url=http://s3.mds.yandex.net s3 ls`

2. залить нужные файлы в бакет диска

про заливку можно почитить тут
https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#primery


### Как загрузить картинки для новой акции

например используя aws

`aws --endpoint-url=http://s3.mds.yandex.net s3 cp grid-promo.png s3://disk/promo/new-year-2022/tuning/grid-promo.png`
`aws --endpoint-url=http://s3.mds.yandex.net s3 cp background-image.jpg s3://disk/promo/new-year-2022/tuning/background-image.jpg`


### Как удалить картинки прошедшей акции

Пример:
`aws --endpoint-url=http://s3.mds.yandex.net s3 rm --recursive s3://disk/promo/new-year-2022/`


### Загружать/удалять картинки для акции можно также через интерфейс

https://yc.yandex-team.ru/folders/foo5clgjfmk87g7nukfd/storage/buckets/disk?key=promo%2F

### Перед тем, как отдать новый json в бекенд нужно его проверить

можно в `src/utils/promoData.ts` добавить поддержку параметра с нужными картинками и текстом

```
if (req.query.theme === 'custom') {
    store.dispatch(setPromoSettings({
        gridCornerPromo: {
            image: 'https://yastatic.net/s3/disk/promo/february-14/web-tuning/grid-promo.png',
            get title() {
                return 'Вы влюбитесь\nв Яндекс 360';
            },
            get description() {
                return 'Скидка 60% до 21 февраля';
            }
        },
        uiTheme: Object.assign({}, darkUiThemePromo, {
            rootBackground: darkUiThemePromo.rootBackground.replace('(url)', `(${'https://yastatic.net/s3/disk/promo/february-14/web-tuning/background-image.jpg'})`)
        })
    }));
}
```
