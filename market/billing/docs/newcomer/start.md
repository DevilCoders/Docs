# Для новых разработчиков Маркет-Биллинга

Тебе уже выдали тикет "Новый разработчик" со списком того, что надо сделать.
Эта страница объясняет, как выполнить какждый из пунктов.

Если тикета у тебя еще нет, попроси своего руководителя выдать. Полезная ссылка для руководителя: [{#T}](../processes/onboarding.md)

**Важно!** Эта страница активно дорабатывается.
Если видишь, что чего-то не хватает, неправильно и т.д. &mdash; пиши комментарий в своем тикете "Новому сотруднику".
Если можешь &mdash; исправляй и дополняй эту страницу тоже.
Советоваться о том, как именно исправить, можно с lena-san@ и sergeitelnov@

## Сделать { #what-to-do }

Если для какого-то пункта нет инструкций или полезных ссылок, смотри страницу на вики: <https://wiki.yandex-team.ru/users/hmepas/market-noobie-howto-draft/>

### Тикет PLANADAPTINTERN { #PLANADAPTINTERN }

Если выдали такой тикет, надо пройтись по чеклисту оттуда.

### Загрузить ssh-ключ на staff { #staff-ssh }

<u>Зачем:</u> Многие внутренние инструменты используют ssh-ключи для аутентификации.

<u>Инструкция:</u> Первые два пункта из <https://wiki.yandex-team.ru/q/devops/faq/generate-and-put-ssh-key/>

<u>Полезные ссылки:</u>

<u>Как проверить успех:</u> Команда `svn ls svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/billing` отрабатывает успешно и показывает список как здесь: <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/>


### Привязать TG-аккаунт на staff { #staff-tg }

<u>Зачем:</u> В чатах есть боты СИБ, которые проверяют, что среди участников только сотрудники Я.

<u>Инструкция:</u>

<u>Полезные ссылки:</u>

<u>Как проверить успех:</u> в анкете на staff видно TG-логин и тулзовые роботы не выгоняют тебя из внутренних чатов


### Подписаться на чаты { #subscribe }

<u>Зачем:</u> Быть в курсе важных и полезных обсуждений

<u>Инструкция:</u>

<u>Полезные ссылки:</u>
* [{#T}](../reference/internal-communications.md)
* <https://wiki.yandex-team.ru/market/development/incident-routing>

<u>Как проверить успех:</u> видишь N новых чатов в TG


### Установить arc { #install-arc }

<u>Зачем:</u> arc &mdash; это яндексовая система контроля версий

<u>Инструкция:</u> <https://docs.yandex-team.ru/devtools/intro/quick-start-guide>

<u>Полезные ссылки:</u>
* <https://wiki.yandex-team.ru/search-interfaces/arc/#ustanovka>

<u>Как проверить успех:</u> команда `arc --help` отрабатывает успешно и выводит справку


### Получить рабочую копию arc { #arc-mount }

<u>Зачем:</u>

<u>Инструкция:</u>

<u>Полезные ссылки:</u>
* <https://docs.yandex-team.ru/devtools/intro/quick-start-guide#mount>
* <https://docs.yandex-team.ru/market-billing/guide/basics/alias> - для удобной работы можно прописать alias.

<u>Как проверить успех:</u> команда `arc branch` выдает какой-то список (если рабочая копия свежая, то в списке только trunk)


### Установить ya { #install-yatool }

<u>Зачем:</u> ya &mdash; внутренняя яндексовая утилита. Через нее делается много всего полезного для разработки.

<u>Инструкция:</u> <https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup> (рекомендуется devtools-ами, но `ya` не будет работать без arc/svn рабочей копии)

<u>Полезные ссылки:</u>
* <https://wiki.yandex-team.ru/yatool/distrib/> (здесь есть вариант без рабочей копии, но только для Linux)

<u>Как проверить успех:</u> команда `ya --help` отрабатывает успешно и выводит справку



### Установить ya-idea { #install-ya-idea }

<u>Зачем:</u> (TODO сформулировать)

<u>Инструкция:</u>
в arc-рабочей копии:

```
cd market/mbi/mbi-tools/arcadia
sudo ./setup.sh  #скопирует скрипт ya-idea в /usr/local/bin
```

Альтернативный вариант, если не хочется трогать системные каталоги:
```
cd market/mbi/mbi-tools/arcadia
vim setup.sh # поменять в строке cp "$(get_arcadia_root)/direct/bin/ya-idea" "/usr/local/bin/ya-idea" последний параметр на что хочешь, например ~/bin (без кавычек, это важно)
./setup.sh
```

<u>Полезные ссылки:</u>
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi-tools/arcadia> -- здесь README про установку скрипта

<u>Как проверить успех:</u> команда `ya-idea -h` отрабатывает успешно и выводит справку (описывает параметры build, open)



### Установить idea и подключить сервер лицензий { #install-idea }

<u>Зачем:</u>

<u>Инструкция:</u>
* Idea скачать и установить с официального сайта, вариант Ultimate <https://www.jetbrains.com/idea/>
* в качестве сервера лицензий указать `https://keys.yandex-team.ru/jetbrains` (либо при старте, либо в меню `Help->Register->License Server`)

<u>Полезные ссылки:</u>
* <https://wiki.yandex-team.ru/jetbrains/licenseservers/>

<u>Как проверить успех:</u> Идея открывается, и в Hepl -> About пишет что она Ultimate, лицензирована на ООО Яндекс

### Настроить Lombok { #configure-lombok }

<u>Зачем:</u> Без плагина среда не будет предлагать методы генерируемые ломбоком

<u>Инструкция:</u> <br/>

Включить обработку аннотаций в Idea: <br/>
Preferences  <br/>
-> Build, Execution, Deployment <br/>
-> Compiler <br/>
-> Annotation Processors <br/>
-> Enable annotation processing <br/> <br/>
Убедиться что установлен плагин **Lombok** для **IntelliJ IDEA**: <br/>
Preferences <br/>
-> Plugins <br/>
-> В поиске набрать "Lombok Plugin" <br/>
-> Нажать Browse repositories... <br/>
-> Выбрать Lombok Plugin <br/>
-> Установить <br/>
-> Перезапустить **IntelliJ IDEA** <br/>

<u>Полезные ссылки:</u> <br/>
Рекомендации к использованию <https://clubs.at.yandex-team.ru/java/985> <br/>
Официальный сайт <https://projectlombok.org/>

<u>Как проверить успех:</u> Использование сгенерированных ломбоком методов не будет гореть красненьким

### Установить Java { #install-java }

<u>Зачем:</u> Некоторые внутренние проекты требуют сертификат Яндекса в джаве.

<u>Инструкция:</u>
`cd ~/arcadia/jdk`
`ya make` (Если добавить `ya make -DJDK_VERSION=15`  (или 8 или 16) то можно получить соответсвующие версии)
Получаешь jdk{version}.tar, его распаковываешь и указываешь как дефолтную jdk

<u>Полезные ссылки:</u>

<u>Как проверить успех:</u> Не будет ошибок из-за сертификатов джавы.

### Сгенерировать проекты для idea, вариант "по проекту на приложение" { #generate-idea-project }

<u>Зачем:</u> (TODO сформулировать честно)

<u>Инструкция:</u>
Генерируем проект для market-billing-tms. В arc-рабочей копии:
```
cd market/billing/market-billing-tms
ya-idea
```

Повторить то же самое для каталогов:
* `market/mbi/mbi/mbi-billing/`
* `market/billing/api/`
* `market/billing/tariffs/`

Красные error в ходе генерации это нормально, если процесс продолжается.

<u>Полезные ссылки:</u>
* <https://wiki.yandex-team.ru/MBI/Development/new_developer/#kakotkrytproektvidea>
* <https://docs.yandex-team.ru/market-billing/guide/basics/arc-begin#primechanie>
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi-tools/arcadia> - Для облегчения генерации проектов.

<u>Как проверить успех:</u> Проекты (из каталога `~/IdeaProjects`) открываются в Идее, в Project Structure видны разумные свойства (например, название в духе `arcadia-market_mbi_mbi`).


### Запустить tms локально { #run-tms }

<u>Что это и зачем:</u> tms (task management system) &mdash; система управления периодическими задачами

<u>Инструкция:</u>
* <https://docs.yandex-team.ru/market-billing/guide/basics/local-tms>

<u>Полезные ссылки:</u>

<u>Как проверить успех:</u> команда `echo 'env type' |nc 127.0.0.1 13713` отрабатывает успешно и выводит `development`


### Запустить тест в Idea { #run-test-idea }

<u>Зачем:</u>

<u>Инструкция:</u> Протестировать mbi-billing тестом FulfillmentOrderBillingServiceDbUnitTest.

<u>Полезные ссылки:</u>
* <https://wiki.yandex-team.ru/MBI/Development/new_developer/#zapusktestovizidea>

<u>Как проверить успех:</u> Тест зеленый


### Запустить тест через ya make { #run-test-ya-make }

<u>Зачем:</u>

<u>Инструкция:</u> TODO рекомендация, какой тест запускать

<u>Полезные ссылки:</u>
* <https://docs.yandex-team.ru/devtools/test/manual>

<u>Как проверить успех:</u> Тест зеленый


### Поломать тест и увидеть, как падает { #break-test }

<u>Зачем:</u>

<u>Инструкция:</u>

<u>Полезные ссылки:</u>

<u>Как проверить успех:</u> Тест был зеленый, после правки стал красный, после отмены правки снова зеленый


### Сделать изменение в логах { #change-log }

<u>Зачем:</u>

<u>Инструкция:</u>
* <https://docs.yandex-team.ru/market-billing/guide/basics/logs>

<u>Полезные ссылки:</u>

<u>Как проверить успех:</u> В логе видно новый текст


### Сделать arc-бранч { #arc-branch }

<u>Зачем:</u> Изучить основные принципы работы с ветками

<u>Инструкция:</u> Открыть документацию маркет-биллинга, страница советы по Аркадии новичкам, найти подпункт
про ветки и ознакомиться с ним.

<u>Полезные ссылки:</u>
* <https://docs.yandex-team.ru/arc/ref/commands#branch>
* <https://docs.yandex-team.ru/market-billing/guide/basics/arc-begin#branch>

<u>Как проверить успех:</u> `arc branch` показывает новый бранч


### Сделать правку в доке { #improve-docs }

<u>Зачем:</u> Научиться работать с документацией

<u>Инструкция:</u> Обратиться к https://staff.yandex-team.ru/lena-san, чтобы узнать, какие статьи можно дополнить, и отредактировать их в веб-интерфейсе или собрать документацию локально (как это сделать описанно в полезных ссылках)

<u>Полезные ссылки:</u>
* <https://docs.yandex-team.ru/market-billing/guide/how-to-write-documentation>

<u>Как проверить успех:</u> правка видна в <https://docs.yandex-team.ru/market-billing/>


### Сделать PR { #pull-request }

<u>Зачем:</u> попробовать полный цикл работы с кодом

<u>Инструкция:</u> Открыть документацию маркет-биллинга, страница советы по Аркадии новичкам, найти подпункт
про сохранение изменений и ознакомиться с ним.

<u>Полезные ссылки:</u>
* <https://docs.yandex-team.ru/arc/ref/commands#pr>
* <https://docs.yandex-team.ru/market-billing/guide/basics/arc-begin#save>
* <https://docs.yandex-team.ru/market-billing/guide/basics/arc-notes>

<u>Как проверить успех:</u> PR видно в списке исходящих ревью в <https://a.yandex-team.ru>

### Получение доступов

<u>Зачем:</u>
* успешно обращаться к бд
* получить админ права

<u>Инструкция:</u>
* [полная инструкция](https://wiki.yandex-team.ru/MBI/Development/new_developer/#polucheniedostupov)
* [как получить доступ к бд и бекофису](https://wiki.yandex-team.ru/MBI/Development/new_developer/#bazyibjekofis)
    * Если поле "стафф" пусто, нажать кнопку 'Я'

<u>Полезные ссылки:</u>
* получение ссылки на заполненную форму в idm:
```
export STAFF=borograam
echo "https://idm.yandex-team.ru/#rf-role=17NqsMjh#user:$STAFF@market_testing/mbi/MBI_DEVELOPER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=E67V29Rk#user:$STAFF@market_testing/mbi/PARTNER_READER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=5g8PSg99#user:$STAFF@market_testing/mbi/ADMIN_READER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=VvyCqrX3#user:$STAFF@market_testing/mbi/ADMIN_REPORTS(fields:(passport-login:yndx-$STAFF);params:()),rf-role=FGwd8u1P#user:$STAFF@market_dev/mbi/MBI_DEVELOPER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=VRRXiJNh#user:$STAFF@market_dev/mbi/PARTNER_READER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=IAfU0l0r#user:$STAFF@market_dev/mbi/ADMIN_READER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=pm0IdlD8#user:$STAFF@market_dev/mbi/ADMIN_REPORTS(fields:(passport-login:yndx-$STAFF);params:()),rf-role=jepiRkEO#user:$STAFF@market/mbi/MBI_DEVELOPER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=OZlubT6r#user:$STAFF@market/mbi/PARTNER_READER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=Z5FUa6AM#user:$STAFF@market/mbi/ADMIN_READER(fields:(passport-login:yndx-$STAFF);params:()),rf-role=hfPkyHKc#user:$STAFF@market/mbi/ADMIN_REPORTS(fields:(passport-login:yndx-$STAFF);params:()),rf-role=Ugv2uxLo#user:$STAFF@ora-billing/all_ro(fields:();params:()),rf=1"
```


### Позадавать запросы к разработческой и тестовой БД { #db-queries-np }

<u>Зачем:</u> увидеть наши данные

<u>Инструкция:</u> [{#T}](../guide/basics/db-queries.md)

<u>Полезные ссылки:</u>

<u>Как проверить успех:</u> Можешь посчитать количество записей в таблице agency.


### Закоммитить себя в группу mbi\_billing
{% note warning %}

Стажёрам выполнять этот пункт не нужно

{% endnote %}

<u>Зачем:</u> Подключиться в группу разработки в аркадии

<u>Инструкция:</u> Группа находится в аркадии [тут](https://a.yandex-team.ru/arc/trunk/arcadia/groups/mbi-billing).
Нужно внести свой логин в группу через стандартную процедуру ПР (создать ветку, внести изменения, запушить ветку в аркадию, создать и влить ПР).

<u>Полезные ссылки:</u>

<u>Как проверить успех:</u> Начнут приходить нотификации по ПР от коллег.

## TODO

Добавить про:
* доступы
* написать какой-нибудь javadoc или комментарий в коде
* заполнить опрос по документации для новеньких
* процесс разработки (для изменений в базе и для тасок)


## Полезные ссылки

__Arc__
* <https://docs.yandex-team.ru/arc/ref/commands>
* <https://docs.yandex-team.ru/devtools/src/arc/workflow>
* <https://wiki.yandex-team.ru/search-interfaces/arc/>


## Возможные проблемы и их решения

### Ошибка при сборке вида Caused by: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested
Обычно связана с установкой стороннего jdk. Необходимо поставить наш сертификат по инструкции отсюда <https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vjava>
