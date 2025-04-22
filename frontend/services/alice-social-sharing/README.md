# Социальная шарилка для запуска навыков Алисы

## Как работает
Поднимется аппхостовая нода и отдает на запросы запроцессенный шаблон. Шаблон является index.html файлом, в который вшиваются стили и javascript. 
Собирается шаблон с помощью webpack, команда `npm run build:client`.

## Запуск
```
npm i
npm run build
npm start
```

### Сгенерировать протобуфный js/ts
```
npm run proto
```

## Локальная разработка

Для локальной разработки есть `webpack-dev-server`. Он рендерит Handlebars шаблоны без бекенда, подставляя моки от
`faker`.

```shell
npx webpack serve --config=webpack.client.js
```

## Разворачивание на дев-тачке

Если нужно поднять сервис на дев-тачке, то есть обёртка, создающая для ОС с systemd сервис и предоставляющая набор
простых операции для управления им (см. `./scripts/service.sh`, для полного списка команд). Для начала, разверните на
дев-тачке репу с кодом и выполните установку:

```shell
./scripts/service.sh install
```

## Тестирование в dev-окружении

Для тестирования необходимо переопределить бекенд `ALICE__SOCIAL_SHARING_FRONTEND` - указав адерс своей dev-тачки в одном из следующих кейсов:

#### В скоупе каталога навыков
Ссылка на каталог на приемке:
`https://priemka.dialogs.alice.yandex.ru/store/skills/7fa868e8-goroda?&srcrwr=ALICE__SKILLS_API_HTTP:fs6yk5odeeaf54cn.sas.yp-c.yandex.net:80&srcrwr=ALICE__NOTIFICATOR_HTTP:notificator.alice.yandex.net:80&srcrwr=ALICE__SOCIAL_SHARING_FRONTEND:nnvle3rtbqdpsb7g.sas.yp-c.yandex.net:10000`

#### В скоупе Литрес
Ссылка на шаринг аудиокниги со странички [аудиокниги](https://www.litres.ru/dmitriy-lipskerov/turisticheskiy-sbor-v-ray-66332022/) на сайте Литрес:
https://dialogs.yandex.ru/sharing/doc?button_text=Слушать&image_url=https%3A%2F%2Fcv2.litres.ru%2Fpub%2Fc%2Fcover%2F66332022.jpg&payload=%7B+%22sharing_user_data%22%3A+%7B+%22user%22%3A+%22630023854%22%2C+%22art%22%3A+66332022%2C+%22time%22%3A+1643640888%2C+%22signature%22%3A+%2260b1e51b97efbbb99a8efb4dd149d49eb1f200ff8f3b07190d8d0b84a9ef562f%22+%7D%7D%27&skill_id=689f64c4-3134-42ba-8685-2b7cd8f06f4d&subtitle_text=Дмитрий+Липскеров&title_text=Туристический+сбор+в+рай&signature=m48kIkak7uWzY7h%2BWwSkOEwbi2wCCXewnWG%2BqAyaIeU%3D&required_interfaces=audio_player&utm_campaign=litres&srcrwr=ALICE__NOTIFICATOR_HTTP:notificator.alice.yandex.net:80&srcrwr=ALICE__SKILLS_API_HTTP:paskills-common-testing.alice.yandex.net:80&srcrwr=ALICE_SOCIAL_SHARE:ebvqgmrqpuvmhvmi.sas.yp-c.yandex.net:10000&srcrwr=ALICE__SOCIAL_SHARING_FRONTEND:nnvle3rtbqdpsb7g.sas.yp-c.yandex.net:10000
#### В скоупе шаринга сценария Генеративных Сказок
Ссылка на документ на приемке:
https://priemka.dialogs.alice.yandex.ru/sharing/doc/PFRPMmRpooQXPq?srcrwr=ALICE_SOCIAL_SHARE:ebvqgmrqpuvmhvmi.sas.yp-c.yandex.net:10000&&srcrwr=ALICE__NOTIFICATOR_HTTP:notificator.alice.yandex.net:80&graphrwr=:social_sharing_send_to_device::trunk&srcrwr=ALICE__SOCIAL_SHARING_FRONTEND:nnvle3rtbqdpsb7g.sas.yp-c.yandex.net:10000
