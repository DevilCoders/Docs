Sitemaps - https://www.sitemaps.org/ru/

Сервис использует технологии:
* [Nirvana](https://nirvana.yandex-team.ru/) для выполнения программного кода.
* [Reactor](https://reactor.yandex-team.ru) для регулярного запуска задач в Nirvana.
* [Lama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama/) для управления реакциями в Reactor.
* [YT](https://yt.yandex-team.ru/docs/) для чтения данных, которые используются в процессе генерации.
* [S3](https://wiki.yandex-team.ru/adfox/mnt/s3-mds/) для хранения Sitemap`ов.

## Как обновить статическую карту ?

### Как обновить через интерфейс арканума ?
1. [Открыть](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/sitemaps/static/craft-ru.csv?edit=true) файл.
2. Сделать изменения.
3. Сохранить изменения:
    * Закомитить изменения.
        <details>
            <summary>Скриншот</summary>
            <img alt="сделать комит" src="https://jing.yandex-team.ru/files/reshetnev-gb/sitemaps-static-commit.png" />
        </details>
    * Создать пулл реквест.
        <details>
            <summary>Скриншот</summary>
            <img alt="создать пулл реквест" src="https://jing.yandex-team.ru/files/reshetnev-gb/sitemaps-static-commit-send-to-review.png" />
        </details>
    * Опубликовать пулл реквест.
        <details>
            <summary>Скриншот</summary>
            <img alt="запаблишить пулл реквест" src="https://jing.yandex-team.ru/files/reshetnev-gb/sitemaps-static-publish.png" />
        </details>
    * Добавить в ревьюверы `sigorilla` или `reshetnev-gb`.
        <details>
            <summary>Скриншот</summary>
            <img alt="добавить ревьюверов" src="https://jing.yandex-team.ru/files/reshetnev-gb/sitemaps-static-review.png" />
        </details>

### Как обновить через arc ?
Когда файл слишком большой, то интерфейс арканума не может с ним работать, поэтому в этом случае обновить/добавить файл нужно через `arc`.

1. [Установить](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#arc-setup) Аркадию.
2. [Получить](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#mount) исходные коды.
3.  <details>
        <summary>Обновить файл</summary>
        Команды по шагам:
        <ul>
            <li>Создать отдельную ветку
            <pre>arc checkout -b any-branch-name</pre></li>
            <li>Поменять файлик
            <li>Сохранить изменения:
                <pre>arc add .
    arc commit -m"Update craft" -n</pre></li>
            <li>Сделать Пулл Реквест: 
                <pre>arc pr create --push --no-edit --publish</pre></li>
            <li>Команда выдаст ссылку на арканум, жмем Ship, жмем Merge</li>
        </ul>
    </details>


## Сущности
* ``Reader`` - сущность которая читает данные из какого-то источника. Например из yt-таблицы.
* ``Landing`` - сущность которая принимает какие-то данные и на основе их может построить/(не построить) лендинг url.
* ``LandingConstraint`` - сущность которая инкапсулирует в себе какое-либо ограничение для построении лендинга.
* ``Printer`` - сущность которая печатает данные куда-то. Например, печатает в текстовый файл, консоль или в sitemap-файл.
