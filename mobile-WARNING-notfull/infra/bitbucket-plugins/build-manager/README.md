# Build manager plugin

1. Плагин берёт статус билдов для PR-в кэша, дополнительно сравнивая значение ревизии с текущим состоянием PR-а (`BuildManagerMergeCheck.preUpdate`). Если в кэше нет данных, то мёрдж всё равно запрещается и стартует конвейер проверок. 
2. Собираем конфиги из pr/merge коммита.
3. Фильтруем билды по затронутым путям в PR: diff(pr/merge->upstream/head).
4. Для каждого отфильтрованного билда достаём последнюю сборку с teamcity.
5. Если сборки нет, триггерим её на pr/merge коммите.
6. Если сборка есть, берём hash1 (на котором она была собрана), берём diff (hash1->pr/merge), проверяем есть ли в diff-е изменения, которые матчатся на эту сборку (и сначала смотрим fast path hash1==pr/merge). Если есть, переходим к шагу 4, если нет, то проставляем зелёный статус.

#### Teamcity WebHook
**Для использования должен быть включен и настроен WebHook на все проекты.**

**Работает работает даже при выключенном плагине.**

Любое сообщение, записанное в лог, начинается с названия класса `TeamcityHookServlet`.
1. На каждое событие, связанное с билдом (started/failed/successful и т.д.), 
[Teamcity WebHook](https://teamcity.yandex-team.ru/webhooks/index.html?projectId=MobileNew_Monorepo) 
посылает POST запрос на URL `$hostname/plugins/servlet/teamcity-hook`, data передается в формате JSON.
2. Эти запросы обрабатываются классом **TeamcityHookServlet** в методе **doPost**.
3. **TeamcityHookServlet** парсит переданный JSON в объект класса **TeamcityJsonData**.
   * Пример минимально необходимого JSON для корректной обработки запроса:  
    ```
    {
        "build": {
            "buildStatus": "Tests passed: 101",
            "buildResult": "success",
            "buildId": "27333259",
            "buildTypeId": "MobileNew_Monorepo_Infra_BitbucketPlugins_Build",
            "teamcityProperties": [
                {
                    "name": "build.vcs.number",
                    "value": "91a32f2e8ca8398c39903b1d131e8d2b8544044f"
                },
                {
                    "name": "teamcity.build.branch",
                    "value": "121/merge"
                },
                {
                    "name": "vcsroot.url",
                    "value": "ssh://git@bb.yandex-team.ru/mobile/monorepo.git"
                }
            ]
        }
    }
    ```
   * Значение свойства `teamcity.build.branch` должно состоять из pull request ID и суффикса "/merge".
   * Значение свойства `vcsroot.url` должно содержать корректную ссылку на VCS root, которая заканчивается на 
   `"/" + project key + "/" + repository slug + ".git"`
   * Элемент `buildStatus` обязателен только если у `buildResult` значение `failure` 
   * Если в JSON'е отсутствует обязательный элемент или один из них не удовлетворяет описанным выше требованиям, то, 
   либо на этапе парсинга, либо в процессе обработки распаршенных значений, возникнет ошибка, которая будет 
   залоггирована, а обработка запроса прервется.
4. По project key, repository slug и pull request ID определяется к какому именно PR'у относится запрос
5. В кэш (buildResultCache) по ключу, состоящему из:
   1. repository ID
   2. pull request ID
   3. значения `buildTypeId`  
   
   кладется значение, состоящее из:
     1. статуса билда, который определяется по значению `buildResult`:
        * `"failure"` -> `TeamcityBuildStatus.FAILURE`
        * `"running"` -> `TeamcityBuildStatus.RUNNING`
        * `"success"` -> `TeamcityBuildStatus.SUCCESS`
        * любое другое значение -> `TeamcityBuildStatus.ERROR`
     2. значения `buildId`
     3. значения `build.vcs.number`
     4. status message, который определяется по значению "buildResult":
        * `"failure"` -> "Build failed: " + значение `buildStatus`
        * `"running"` -> "Build in progress"
        * `"success"` -> "Build successful"
        * любое другое значение -> "ERROR"
6. И ключ и значение логируются в форме `Build info put to the cache: repoId={}, prId={}, 
buildTypeId={}, status={}, buildId={}, mergeHash={}, statusMessage={}`.
7. Если возникнет ошибка в процессе парсинга JSON'а, код ответа будет **400** (`SC_BAD_REQUEST`).  
Иначе (в любом случае) код ответа будет **204** (`SC_NO_CONTENT`).


#### PullRequestEventListener
**Не работает при выключенном плагине.**  
Любое сообщение, записанное в лог, начинается с названия класса, в котором происходят описанные действия.  
1. **PullRequestEventListener** ловит события, связанные с PR (не ловит события по закрытым PR). 
Если событие связано с открытием PR, изменением в ветке или изменением target branch, то инициируется событие **MergeCommitChangedEvent**.   
2. **MergeCommitChangedEventListener** проверяет наличие токена в настройках битбакета и запускает обработку конфигов проектов в репозитории. 
Если токена нет, то ошибка "No TC token" логируется, кладется в `pullRequestErrorCache` (ключ **PullRequestStateCacheKey** состоит из repository ID, pull request ID и mergeHash) и работа прекращается. 
Если токен есть, то запускается **ConfigProcessor**.
3. **ConfigProcessor** парсит все конфиги и возвращает отфильтрованный по измененным путям и target branch список билд-конфигов (подробнее с видом конфигов и правилами фильтрации можно ознакомиться по ссылке https://wiki.yandex-team.ru/mobvteam/build-manager/). 
Если **ConfigProcessor** отработал с ошибкой, то **MergeCommitChangedEventListener** кладет в `pullRequestErrorCache` ошибку, логирует ее и дальше не идет. 
Ошибкой может быть одна из следующих (**ExceptionMessages**):
   * "Config %s format is wrong";
   * "Root config format is wrong";
   * "Project config %s is empty";
   * "There are no TC builds in configuration of project %s";
4. Если **ConfigProcessor** вернул список билд-конфигов, то они записываются в `buildListCache` (ключ **RepoPrCompositeKey** состоит из repository ID, pull request ID) и, если этот список непустой, инициируется событие **PullRequestPreparedEvent**.
5. **PullRequestPreparedEventListener** проверяет наличие сборки в `buildResultCache` (ключ **BuildResultCacheKey** состоит из repository ID, pull request ID и buildTypeId, значение **TeamcityBuildResult** состоит из status, buildId и mergeHash). 
Если сборки нет, она триггерится на pr/merge коммите. Запуск логируется в **PullRequestPreparedEventListener** и записывается в `buildResultCache` со статусом `queued`.
6. Если сборка есть, берётся hash1 (на котором она была собрана) и diff (hash1->pr/merge), смотрится fast path hash1==pr/merge, затем проверяется есть ли в diff-е изменения в путях, по которым должна запускаться сборка. 
Если есть, то запускается новый билд, запуск логируется в **PullRequestPreparedEventListener** и записывается в `buildResultCache` со статусом `queued`. Если нет, то в `buildResultCache` проставляется новый mergeHash равный pr/merge. 
7. Если не удалось запустить билд по причине невалидного токена, то в `pullRequestErrorCache` кладется соответствующая ошибка. 
Если по каким-либо другим причинам, то ошибка кладется в информацию по конкретному билду в `buildResultCache`. Обе ошибки логируются в **PullRequestPreparedEventListener**.


#### Merge check
Любое сообщение, записанное в лог, начинается с названия класса `BuildManagerMergeCheck`.
1. При каждом обновлении страницы PR'a или обработке запроса на merge вызывается метод **preUpdate**
класса **BuildManagerMergeCheck**
(from [official website](https://developer.atlassian.com/server/bitbucket/tutorials-and-examples/controlling-when-pull-requests-can-be-merged/):
_This method is called when Bitbucket Server is either in the process of handling
a request to merge a pull request or it wants to display to the user whether the pull request can be merged_).
2. Первым делом проверяется включен ли плагин для репозитория, в котором лежит target branch: вызывается метод
**isEnabled** класса **BuildManagerPluginSettings**. Если плагин выключен, в лог пишется сообщение в форме 
`BuildManagerMergeCheck .preUpdate triggered, but plugin is disabled for repository with id={}`, merge **запрещается**
(`PLUGIN_DISABLED`). 
Это означает, что для репозитория выключен плагин, но включен merge check. Рекомендуется не допускать таких ситуаций.
   * включить/выключить плагин: Repository settings -> General -> Enable build manager (checkbox).
   * включить/выключить merge check: Repository settings (Project settings) -> Merge checks -> Build Manager Merge Check
3. Из кэша skipChecksOnceCache достается статус пропуска проверок. Если для текущего PR нужно пропустить все проверки
(ранее была нажата кнопка `Skip checks once` и с того момента изменений в ветке (и апстриме) не было), в лог пишется
сообщение в форме `Checks skipped for pull request with id={}`, merge **разрешается** (`ACCEPTED`) и больше merge check
ничего не делает.
4. Если скипа не было, то проверяется наличие ошибок в pullRequestErrorCache (ключ состоит из repository ID, pull request ID и mergeHash). 
Если ошибка есть, то merge **запрещается** (`REJECTED`)
5. Из кэша (buildListCache) достается список билдов для текущего PR'а. Если списка в кэше не оказалось, 
публикуется event (класс **MergeCommitChangedEvent**). Метод **onApplicationEvent** класса **MergeCommitChangedEventListener** 
обрабатывает этот event и кладет список билдов в кэш. **MergeCommitChangedEventListener** работает в другом потоке,
так что может не успеть посчитать список билдов за время исполнения merge check.
6. Из кэша (pullRequestStateCache) достается state для текущего PR'a по ключу (ключ состоит из repository ID, pull request ID и mergeHash). 
Если state в кэше не оказалось или он неактуален (текущий merge branch hash не равен merge branch hash на момент последнего вычисления state), state 
вычисляется. А именно: 
   * если список билдов (см. п. 4) не известен (=`null`) для PR'а, `state.status` = `BuildListStatus.PENDING`
   * если все билды актуальны и их статус `TeamcityBuildStatus.SUCCESS`, `state.status` = `BuildListStatus.OK`
   * иначе `state.status` зависит от первого билда со статусом не `TeamcityBuildStatus.SUCCESS`, который мы встретим
при их обходе:
   * если статус билда неизвестен или неактуален, `state.status` = `BuildListStatus.PENDING`
   * если билд ещё не завершился (его статус `TeamcityBuildStatus.RUNNING`), status = `BuildListStatus.RUNNING`
   * если статус билда `TeamcityBuildStatus.ERROR`, `state.status` = `BuildListStatus.FAILED`.  
Полученный state кладется в кэш.
7. Если при обходе один из билдов имеет статус `TeamcityBuildStatus.RUNNING`, то создается событие **CheckBuildListStatusEvent**.
**CheckBuildListStatusEventListener** проверяет наличие записи в `buildListCache`, если ее нет, то создается событие **MergeCommitChangedEvent**.
Если есть, то проверяется наличие записи в `buildResultCache`. 
Если ее нет, то запускается новый билд, запуск логируется в **CheckBuildListStatusEventListener** и записывается в `buildResultCache` со статусом `queued`.
Если есть, то проверяется статус билда. Если состояние билда `TeamcityBuildState.finished` и статус не соответствует тому, который лежит в кэше, то он перезаписывается.
8. Делается запись в лог в форме `PR id: {}, status: {}, merge commit: {}`.
9. По значению `state.status` определяется результат работы merge check'а:
   * если `state.status` = `BuildListStatus.OK`, merge **разрешается** (`ACCEPTED`)
   * если `state.status` = `BuildListStatus.PENDING` или `state.status` = `BuildListStatus.RUNNING`,
   merge **запрещается** (`PENDING`)
   * в любом другом случае merge **запрещается** (`REJECTED`).

