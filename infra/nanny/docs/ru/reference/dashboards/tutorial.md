# Туториал по дашбордам

## О дашбордах {#about}

Дашборды задуманы как средство для удобного просмотра и управления множеством сервисов.

В данный момент дашборды предоставляют следующие возможности:

* просмотр состояния сервисов, входящих в дашборд;
* группировка сервисов по ярлыкам, по версии ресурсов (поддержаны Sandbox- и URL-файлы), и их комбинациям;
* «ручное» массовое обновление: при группировке по версии ресурса, можно обновить ресурс одновременно у всех сервисов, входящих в группу;
* «автоматизированное» массовое обновление: возможность применять релизы к группам сервисов;
* выполнение мета-рецептов: массовой выкладки новых ревизий сервиса по заданному сценарию.

В данном документе мы постараемся рассказать об основных возможностях и показать, как ими пользоваться.

## Создание {#creation}

На видео показана процедура создания дашборда.

<iframe height="400" width="100%" frameborder="0" src="https://jing.yandex-team.ru/files/romanovich/create.mp4"></iframe> 

Заполняем идентификатор, имя и описание. В качестве владельца оставляем подставленного по умолчанию текущего пользователя, в качестве менеджеров указываем группу со Стаффа. Единственное отличие между владельцами и менеджерами пока заключается в том, что владельцы дашборда могут его удалить.

Затем мы создаём группу stable, добавляя в неё один сервис, и группу prestable, добавляя в неё несколько сервисов. Стоит отметить, что виджет позволяет выбирать не только отдельные сервисы, но и категории целиком.

Перетащив один сервис из prestable в stable, а один — из prestable в корзину, мы нажимаем  **Create** и переходим на страницу свежесозданного дашборда.

## Редактирование {#editing}

Создав дашборд, мы можем его отредактировать, добавив ещё одну группу — testing, состоящую из двух сервисов.

<iframe height="400" width="100%" frameborder="0" src="https://jing.yandex-team.ru/files/romanovich/edit.mp4"></iframe> 

## Labels {#labels}

**Labels** — это набор пар ключ-значение, которые можно указать в настройках дашборда на странице редактирования. Например, для дашборда `noapache_imgs` можно указать следующий набор:

```
{
  "team": "marty",
  "vertical": "imgs"
}
```
Т.е. указать, что отвественная команда — MARTY (группа выполнения регламентных работ), поисковая "вертикаль" — Картинки.
Label'ы используются в данный момент для следующего:

* При старте мета-рецепта все label'ы дашборда указываются в качестве label'ов результирующей выкладки — таскгруппы.
После этого мы можем фильтровать такие таскгруппы, например, создав панель задач — [task panel](../alemate/task_panels.md).

## Динамическая группировка по ресурсу {#group-by-resources}

Стоит отметить, что созданные нами группы являются лишь группировкой по умолчанию, предназначенной для удобства пользователей, и могут называться как угодно.

Основная польза от дашбордов заключается в возможности задавать динамическую группировку. Например, по ресурсу. В данном видео показано, как мы:

* оставляя группировку по умолчанию, группируем по ресурсу `app` (то есть, версии приложения);
* снимаем группировку по умолчанию, оставляя группировку по `app`;
* группируем по `instancectl`.

<iframe height="400" width="100%" frameborder="0" src="https://jing.yandex-team.ru/files/romanovich/group-by-resource.mp4"></iframe> 

## Обновление ярлыков сервисов {#update-service-labels}

Сервису в Няне можно присвоить ярлыки (labels). Ярлык представляет собой пару ключ-значение, например, `{geo: msk}` или `{ctype: stable}`.
В нашем дашборде возможность сгруппировать сервисы по ярлыкам пока что отсутствует, так как они не указаны ни в одном из его сервисов.

Мы переходим на страницу demo_service_1 и, чтобы не вбивать ярлыки руками, нажимаем кнопку **Update Service Labels**. Няня пересекает теги инстансов текущей активной конфигурации, ищет в получившемся множестве теги вида `a_geo_*`, `a_itype_*` и так далее, и на основе полученной из них информации обновляет ярлыки сервисов.

Чтобы не повторять эту процедуру для каждого из оставшихся пяти сервисов, на странице дашборда мы нажимаем **Actions → Update Service Labels**, тем самым обновляя ярлыки всех сервисов, входящих в дашборд.

После этого мы можем видеть имена ярлыков в выпадушке селектора группировки на странице дашборда.

<iframe height="400" width="100%" frameborder="0" src="https://jing.yandex-team.ru/files/romanovich/update-labels.mp4"></iframe> 

## Динамическая группировка по ярлыкам {#group-by-labels}

В этом видео мы:

* группируем по ярлыку `geo`;
* группируем по паре ярлыков `(geo, itype)`;
* группируем по паре ярлыков `(geo, itype)` и ресурсу `instancectl`;

<iframe height="400" width="100%" frameborder="0" src="https://jing.yandex-team.ru/files/romanovich/group-by-labels.mp4"></iframe> 

## Массовое обновление ресурса {#mass-resource-update}

Имея группировку по ресурсу, мы можем обновить его версию сразу во всех сервисах, входящих в группу.

Мы группируем по `instancectl`, сбрасываем группировку по умолчанию, нажимаем в заголовке группы кнопку **Edit Resource**, выбираем новую версию, нажимаем Save.
В появившемся модальном окне мы видим дифф, список сервисов, подпадающих под планируемое изменение, и поле для ввода комментария к коммиту. Проверив, что нас всё устраивает, мы нажимаем **Continue**.

После этого мы видим новый снапшоты в сервисах `demo_service_3` и `demo_service_4`. У снапшота мы можем нажать кнопку **Change** и изменить его target state на ACTIVE, тем самым инициировав его выкладку.

<iframe height="400" width="100%" frameborder="0" src="https://jing.yandex-team.ru/files/romanovich/batch-update.mp4"></iframe> 

## Массовое применение релизов {#mass-release-apply}

Релиз из Sandbox, попадая в Няню, порождает [release](https://nanny.yandex-team.ru/ui/#/releases/?filter=status%3DOPEN). Если в сервисе настроена tickets integration и заведены релизные правила, срабатывающие на этот релиз (как это [сделано для наших тестовых сервисов](https://nanny.yandex-team.ru/ui/#/services/catalog/demo_service_1/tickets_integration)), Няня породит тикет, привязанный к сервису.

В дашборде для каждой группы (будь то группы по умолчанию или динамической) справа показывается список тикетов, подходящих к сервисам группы, сгруппированный по родительским релиз-реквестам.

На данном видео мы можем видеть три релиз-реквеста — stable, prestable и unstable. У каждого из них есть два дочерних тикета.

Мы сбрасываем группировку, тем самым создавая группу, в которую входят все сервисы. Выделяя stable релиз-реквест, мы видим, что сервисы отфильтровались и остались только те, для которых выделенный релиз реквест актуален. Выделяя testing релиз-реквест, видим то же самое. Для него мы нажимаем кнопку Activate, выбираем activate-рецепты, нажимаем **Apply** и наблюдаем за процессом выкладки сервисов.
[Видео](https://jing.yandex-team.ru/files/romanovich/apply-rr.mp4)

