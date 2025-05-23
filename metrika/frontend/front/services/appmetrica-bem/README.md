Начало разработки
---------------

Заходим на дев машинку:

    ssh appmetrika01k-dev.man.yp-c.yandex.net

Генерируем и добавляем свой ключ в гитхаб (https://github.yandex-team.ru/settings/ssh):

    ssh-keygen -t rsa # много раз ентер
    cat ~/.ssh/id_rsa.pub`

Дальнейшая сборка и запуск описаны в корне репозитория:
```
npm run bootstrap -- --scope=appmetrica-bem
npm run l appmetrica-bem
```

Сайт будет доступен по адресу `mono-<app>-<user>.appmetrika-dev.haze.yandex.ru`

Разработка
---------------

Актуальной, стабильной веткой счиатется develop

Небольшая сборка ссылок по разработке проекта доступна [тут](https://wiki.yandex-team.ru/users/mdidkivskyi/appmetrika)

Сборка умеет автоматически инлайнить картинки - необходимо добавить параметр `appmetrica_inline_image` в `url`. Например:

    background-image: url('icon.(svg|png|jpg)?appmetrica_inline_image=1');

При сборке пакета такая иконка будет заинлайнена, а для `svg` еще и запущен `svgo`. При разработке этого не происходит.

Структура БЭМ части проекта
---------------
 * `autobuild_blocks` сгенерированные данные для других блоков, например список таймзон и выходные дни. автогенерируется

структура `blocks/`

 * `blocks/api` блоки, которые предоставляют интерфейс на получение данных из внешних источников (бекенда)
 * `blocks/common` блоки, не имеющие DOM-представления, обычно всякие helper-блоки
 * `blocks/data` блоки, специально для получения данных их API (используя ctx.defer())
 * `blocks/desktop` основые блоки, внутри обычно шаблоны, css и браузерная js-часть
 * `blocks/external` подключение внешних библиотек в бэм-сборку
 * `blocks/inherits` расширение внешних блоков и библиотек
 * `blocks/models` [модели](https://github.com/bem-node/bem-promised-models/)
 * `blocks/pages` контролеры страниц

Дополнительные команды
--------------- 

Для запуска проекта с поддержкой Node Inspector (Debugger), нужно запускать приложение с флагом `NODE_INSPECT`, например `NODE_INSPECT=1 npm run ...`. Также потребуется прокинуть порт дебаггера на локальную машину. Находим в консоли последнее сообщение с адресом дебагера, копируем адрес в браузер (адрес вида chrome-devtools://...). Пробрасываем порт из адреса в ssh (`ssh -L <port>:127.0.0.1:<port> appmetrika-dev-trusty.mtrs.yandex.ru`).

Обновление переводов. В качестве параметра можно передать имя блока/блоков (именно имя, а не путь), чтобы не скачивать все переводы

    npm run i18n -- --blocks=block1,block2

Тесты
------------

Тесты запускаются коммандами `npm test` и `npm run test:watch`
Для тестов используется набор: jest, enzyme
