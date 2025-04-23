# Как писать storybook-тесты

По всем вопросам пишите в [чат поддержки в Telegram](https://t.me/joinchat/4EnOqu8kP7QwNmZi)

{% note warning %}

Написание storybook-тестов поддерживается только локально. На виртуалках QYP не работает.

{% endnote %}

## [Я не хочу ничего читать и генерировать, хочу написать просто скриншотный тест](#fast-recipes)

## Соглашения
### Термины
`Тестовая story` - это компонент, отрендеренный в storybook, для которого автоматически запускается проверка скриншотом с помощью hermione. Все story, написанные по правилам из этой инструкции – это тестовые story.

`Test config` – это файл `test.config.js`, в котором указаны настройки для снятия фикстуры.

`Фикстура (fixture)` – это дамп определённого стостояния Redux Store, записанный в файл `fixture.json.gz`. Фикстуры используются автоматически при их наличии в папке c тестовой story. Они хранятся в `git lfs` и автоматически подтягиваются   и распаковываются при запуске storybook.

### Файловая структура:
Тестовые story располагаются в DNA определённым образом. Это позволяет сократить количесто сущностей, необходимых для теста и всячески автоматизировать процесс написания и запуск  storybook-тестов.

Все тестовые story должны лежать в папке `stories` внутри папки тестируемого компонента. Тестовые стори добавляются в папку `stories` в виде папки с названием, которое будет использоваться в качесте имени story в storybook и теста в hermione:
```
<ComponentDir>/
    stories/
        testName1/
            story.tsx
            test.config.js
        testName2/  
            ...
```

## Настройка IDE Webstorm для быстрого создания шаблонов тестов { #ide-config }

Заходим в настройки IDE - Tools
![картинка](https://jing.yandex-team.ru/files/gorbatov/step1.png)

Создаем новый элемент
![картинка](https://jing.yandex-team.ru/files/gorbatov/step2.png)

Заполняем настройки первой команды

Name - `Create default storybook`

Program - `$ProjectFileDir$/scripts/create-default-storybook.js` или абсолютный путь для запуска из монорепозитория `/Users/LOGIN/arcadia/adv/frontend/services/dna/scripts/create-default-storybook.js`

Arguments - `$FileDir$`

Working directory - `$ProjectFileDir$`
![картинка](https://jing.yandex-team.ru/files/gorbatov/step3.png)

Заполняем настройки второй команды

Name - `Create storybook fixture`

Program - `$ProjectFileDir$/scripts/create-storybook-fixture.js` или абсолютный путь для запуска из монорепозитория `/Users/LOGIN/arcadia/adv/frontend/services/dna/scripts/create-storybook-fixture.js`

Arguments - `$FileDir$`

Working directory - `$ProjectFileDir$`
![картинка](https://jing.yandex-team.ru/files/gorbatov/step4.png)


Для команды создания типизированной фикстуры `Create storybook typed fixture` настройки почти такие же, кроме поля Program:

`$ProjectFileDir$/scripts/create-storybook-typed-fixture.js` или абсолютный путь для запуска из монорепозитория `/Users/LOGIN/arcadia/adv/frontend/services/dna/create-storybook-typed-fixture.js`

![картинка](https://jing.yandex-team.ru/files/gorbatov/typed1.png)


Далее можно вызвать нужные команды из контекстного меню папки компонента

![картинка](https://jing.yandex-team.ru/files/gorbatov/step5.png)

После этого будет создан дефолтный тест и в нем нужно настроить нужные поля стейта (см. ниже) для фикстуры и можно создать фикстуру через контекстное меню папки теста

 ![картинка](https://jing.yandex-team.ru/files/gorbatov/step6.png)

 или типизированную фикстуру

![картинка](https://jing.yandex-team.ru/files/gorbatov/typed2.png)

## Настройка IDE VSCode для быстрого создания шаблонов тестов { #ide-vscode-config }

Скачиваем плагин - https://marketplace.visualstudio.com/items?itemName=edonet.vscode-command-runner

В проект .vscode/settings.json добавляем:

```
{
    "command-runner.terminal.name": "runCommand",
    "command-runner.terminal.autoClear": true,
    "command-runner.terminal.autoFocus": true,
    "command-runner.commands": {
        "Create default storybook": "./scripts/create-default-storybook.js ${fileDirname}",
        "Create storybook fixture": "./scripts/create-storybook-fixture.js ${fileDirname}",
        "Create storybook typed fixture": "./scripts/create-storybook-typed-fixture.js ${fileDirname}",
    },
}
```

После этого можно вызывать эти команды в контекстном меню файла для теста, который должен быть открыт (это важно для формирования пути!):

![картинка](https://jing.yandex-team.ru/files/gorbatov/vscode-1.png)

И вызывать нужную:

![картинка](https://jing.yandex-team.ru/files/gorbatov/vscode-2.png)

Для фикстуры нужно открыть файл с тестом (это важно для формирования пути!):

![картинка](https://jing.yandex-team.ru/files/gorbatov/vscode-3.png)

Также:

![картинка](https://jing.yandex-team.ru/files/gorbatov/vscode-4.png)

### Запуск
#### Точка входа в storybook-тесты:
`npm run storybook -- --help` – выведет описание доступных команд. Запуск не тестового storybook работает по-прежнему.

#### Запуск storybook отдельно: { #standalone-storybook-run }
`npm run storybook` – запустит и откроет в браузере storybook cо всеми тестовыми story.

`npm run storybook [grep]` - для выборочного запуска storybook предусмотрен позиционный аргумент. Логика работы такая же как и у `npm run storybook test [grep]`

Например:

`npm run storybook src/containers` – запустит все тестовые story внутри `src/containers`

`npm run storybook containers` – запустит все тестовые story внутри всех папок `containers` в проекте

`npm run storybook <путь до папки с компонентом или название папки с компонентом>` – запустит все тестовые story для выбранного компонента

`npm run storybook <путь до папки в stories>` – запустит только выбранную тестовую story

`npm run storybook <grep тестов из gui>` – запустит только тестовые story выбранных тестов


Все вышеперечисленные команды запускают только тестовые стори. Для включения запуска старых `.stories.tsx` нужно добавить флаг `-l` (`--legacy`).
Например, чтобы запустить все story (тестовые и старые) из папки `src/components`:

`npm run storybook src/components -- -l`

#### Запуск storybook тестов:
`npm run storybook test` – запустит storybook, если он ещё не запущен, запустит hermione GUI. По-умолчанию в GUI будут отображены все тестовые story в DNA. Тесты будут запущены на удалённом selenium grid.

`npm run storybook test [grep]` – то же что и без `grep`, но в GUI будут отображены только сматченные тестовые story. В качестве `grep` подойдёт греп тестовой story из отчёта hermione или путь до папки с тестовой story.

`pnpm run storybook test -- --from=https://proxy.sandbox.yandex-team.ru/2699818935/index.html` - запуск тестов с переиспользованием готового CI-отчёта. Удобно, когда на CI уже есть отчет и нужно принять новые скриншоты. 

#### Снятие фикстуры для тестовой story:
`npm run storybook fixture [grep]` – запустит локальный selenium, запустит hermione, которая выполнит сценарий, описанный в `test.config.js`. По-умолчанию сценарий выполнится в локальном браузере.
Запуск возможен только для определённых тестовых story, поэтому необходимо указать `grep`. Подходящие для `grep` значения такие же, как и для тестовой story. Результат работы команды – это файлы `fixture.json.gz` и `fixture.json`, записанные в папку с тестовой story.

#### Генерация бойлерплэйта для новой тестовой story: { #boilerplate-for-new-story }
`npm run storybook add` – задаст пару вопросов, нужно ввести путь к папке с тестируемым компонентом и название тестовой story. Если в вашей ветке есть изменённые .tsx файлы – предложит их папки для генерации файловой структуры тестовых story.

`npm run storybook add [path]` – создаст тестовую story с названием `default` в папке `path` минуя диалог.

`npm run storybook add [path] -- -t customTestTitle` – создаст тестовую story с названием `customTestTitle` в папке `path` минуя диалог.

## Тестовые story компонентов (не используют Store)
API создания тестовых story отличается от API storybook 5, которое используется в DNA для написания `*.stories.tsx`

Для того, чтобы написать тестовую story компонента, нужно:
- создать папку `stories` в папке компонента. Для этого и сдедующих трёх шагов можно использовать скрипт генерации новой тестовой story `npm run storybook add`
- в папке `stories` создать папку, с названием, которое отражает определённое состояние компонента, название должно быть написано `латиницей в camelCase` – это назание вашей тестовой story, под капотом используется как первый аргумент для функции [storiesOf(...).add](https://github.com/storybookjs/storybook/blob/next/lib/core/docs/storiesOf.md)
- в созданой папке создать файл `story.tsx` – это и есть тестовая story. [Пример файла story.tsx](https://github.yandex-team.ru/direct/dna/blob/master/src/components/Alert/stories/typeError/story.tsx)
- экспортировать из файла `story.tsx` функцию,  которая возвращает объект с интерфейсом `AddStory`
- в возвращаемый объект добавить поля:
    - `getComponet`: функция, которая возвращает тестируемый компонент в нужном состоянии. Под капотом используется как второй аргумент функции [storiesOf(...).add](https://github.com/storybookjs/storybook/blob/next/lib/core/docs/storiesOf.md)
    - [опционально] `parameters`: объект с параметрами для декораторов storybook. Под капотом используется как третий аргумент функции [storiesOf(...).add](https://github.com/storybookjs/storybook/blob/next/lib/core/docs/storiesOf.md)
    - [опционально] `decorators`: массив кастомных декораторов для story.
    - [опционально] `wrapperStyle`: объект с СSS стилями для обёртки вокруг компонента. Под капотом обёртка имеет css класс `.story-wrapper`, который используется для снятия скриншота
- запустить storybook командой `npm run storybook [путь к тестовой стори (copy relative path в WS или VSCode)]` и проверить, что компонент отображается правильно.
- запустить storybook-тест этого компонента по грепу. `npm run storybook test [путь к тестовой стори (copy relative path в WS или VSCode)]`
- запустить тест через GUI и принять скриншот. Скриншот появится в папке тестовой story.
- Готово. Осталось только закоммитить.

## Тестовые story контейнеров, использующие генератор стейта и типизированне стабы (предпочтительный способ) { #typed-fixture }

Можно написать сторибук-тест на контейнер, создав стейт для него с помощью генератора. Генератор стейта - это функция `getFixtureState` (https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna/src/test-utils/stateHelpers/getFixtureState.ts), в которой можно сконгфигурировать стейт без json-фикстуры.

Данный стейт передается в тест с помощью параметра `store`:

```
import { getFixtureState } from '@/test-utils/stateHelpers/getFixtureState';

export default (): AddStory => ({
    getComponent: () => (
        <PlatformSelectorEditorContainer campaignId={campaignId} editorId={`campaign-${campaignId}strategy`} />
    ),
    reducers: {
        strategyEditor: strategyEditorReducer
    },
    state: getFixtureState({
        client: YUBER,
        features: [[FeatureName.SOCIAL_ADVERTISING, true]],
        stubs: {
            strategyEditor: {
                editors: {
                    [campaignId]: {
                        platform: CampaignPlatform.BOTH
                    }
                }
            },
            editCampaigns: {
                editors: {
                    [campaignId]: {}
                }
            }
        }
    })
});
```
Метод принимает следующие параметры:
- `client` - текущий клиент.
- `features` - список переопределенных фич для оператора и клиента.
- `stubs` - генераторы частей стейта или стабы. На данный момент есть стабы-генераторы для metrikaCounterEditor, siteCallTrackingEditor, editCampaigns, campaignLink, strategyEditor.
- `overrides` - "грубые" переопределения частей стейта (лучше дописать нужный стаб-генератор).

Если вам нужен стаб, которого сейчас нет в списке, то нужно его создать и положить в https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna/src/test-utils/stateHelpers/stubs. Стабы - это  довольно простые функции по генерации стейта на основе каких-то базовых параметров. Стаб-функции должны возращать тип `State[key]`, например:

```
const assetButtonEditorFixture = (settings?: AssetButtonEditorsStubSettings): State['assetButtonEditor'] => {
    ...
}
```

Чтобы получить шаблон стаба для теста нужно создать сторибук-тест, сконфигурировать его через `test.config.js` и вызвать, например, для теста src/containers/CampaignMetrikaCounterEditorContainer/stories/readOnly (снимаем стейт с локально-запущенного dna):

`pnpm run storybook fixture src/containers/CampaignMetrikaCounterEditorContainer/stories/readOnly -- --use-typed-mocks --p 3000`

или команду `Create storybook typed fixture` для [Webstorm]( #ide-config ) и [VScode]( #ide-vscode-config )

Команда прочтёт конфиг в находящемся рядом test.config.js и попробует создать типизированный кусок стейта. Из него нужно скопировать нужное, типизировать окончательно (автоматика лажает для сложных типов) и создать универсальный стаб-генератор, которым смогут воспользоваться другие. Созданные stateFixture.ts и test.config.js можно потом удалить.

## Тестовые story контейнеров (мокают Store c помощью json-фикстуры)

[Лучше использовать типизированную фикстуру]( #typed-fixture )

Тестовые story контейнеров пишутся также как и тестовые story компонентов. Разница только в том, что для контейнера нужно сохранить новую фикстуру или переиспользовать готовую из соседней тестовой story.

### Чтобы сохранить фикстуру, нужно:
- найти в интерфейса DNA с базой `devtest` страницу, на которой достижимо желаемое состояние тестируемого контейнера.
- cоздайть в папке с тестовой story файл `test.config.js`. [Пример файла test.config.js](https://github.yandex-team.ru/direct/dna/blob/master/src/containers/StrategiesEditorForCampaignEditContainer/stories/simpleModeCPC/test.config.js)
- экспортировать из него объект с полем `fixture`
- заполнить поля у объекта `fixture`:
  - `url`: url найденной страницы (без хоста)
  - `waitForReady`: функция для hermione – сценарий достижение желаемого состояний контейнера. Или `await browser.debug()`, чтобы накликать состояние вручную.
  - `storeParts`: объект-декларация, какие поля из стора необходимы для контейнера. Поддерживает вложенные объекты. Чтобы получить поле целиком, укажите для этого поля `null`. Весть Store задампить нельзя.
  - [опционально] `features`: включить или выключить фичи, специфичные для желаемого состояния контейнера. Дополняет список из [defaultFeatures](https://github.yandex-team.ru/direct/dna/blob/master/.config/hermione/lib/overrideFeatures.js#L7) в рантайме.
- запустить генерацию фикстуры `npm run storybook fixture [путь к тестовой стори (copy relative path в WS или VSCode)]`. Если в сценарии `waitForReady` есть `await browser.debug()`, то выполнение сценария на этом месте остановится. Нужно накликать нужно состояние приложения в интерфейсе DNA и перейти к записи фикстуры, продолжив выполнение сценария (в терминале дважды нажать `ctrl + c` или ввести `.exit`). После завершения сценария фикстура запишется в файл `fixture.json.gz` (для хранения в git lfs) и распакуется как `fixture.json` – для просмотра содержимого и для использоования в тестовой story.
- убедиться, что всевозможные id в ownProps контейнера в файле `story.tsx` соответствуют id из фикстуры (можно зареквайрить их из фикстуры) 
- запустить storybook командой `npm run storybook [путь к тестовой стори (copy relative path в WS или VSCode)]` и проверить, что компонент отображается правильно.

### Чтобы переиспользовать фикстуру, нужно: { #reuse-fixture }
добавить в папку с тестовой story  файл `fixture.js` ([пример](https://github.yandex-team.ru/direct/dna/blob/master/src/containers/BannerLinkEditorForEditBannerContainer/stories/hasSelectOpen/fixture.js)):
```
export const fixture = require('../<другая тестовая стори>/fixture.json');
```
При переиспользовании фикстуры 1 в 1 новое состояние достигается при помощи гермионы.
Нужно добавить сценарий в файл `test.config.js` ([пример](https://github.yandex-team.ru/direct/dna/blob/master/src/containers/BannerLinkEditorForEditBannerContainer/stories/hasSelectOpen/test.config.js))

Также при переиспользовании фикстуры можно переопределить поля возвращаемого объекта, чтобы получить новое состояние: [пример](https://github.yandex-team.ru/direct/dna/blob/master/src/containers/StrategiesEditorForCampaignEditContainer/stories/simpleModeCPANoGoals/fixture.js)

## Я не хочу ничего читать и генерировать, хочу написать просто скриншотный тест { #fast-recipes }

Для перечисленных ниже команд можно настроить быстрый вызов в [Webstorm]( #ide-config ) и [VScode]( #ide-vscode-config )

В проекте есть два актуальных вида сторибуков:

1) 1 файл - много сторибуков (более универсальный способ, который используется в других проектах)
2) 1 файл - 1 сторибук

# Cоздание тестов первого типа

Рядом с компонентом создаем папку stories, в неё добавляем файл ComponentName.new.story.tsx. 

Примеры: 
- [CampaignMetrikaCounterEditorContainer.new.story.tsx](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna/src/containers/CampaignMetrikaCounterEditorContainer/stories/CampaignMetrikaCounterEditorContainer.new.story.tsx)
- [OverviewTooltipPromoContent.new.story.tsx](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna/src/components/OverviewTooltipPromoContent/stories/OverviewTooltipPromoContent.new.story.tsx)

Запуск таких сторибуков производится командой `pnpm storybook:start:new`, а ручной прогон hermione-тестов на них - командой `pnpm hermione:manual`

Для таких сторибуков можно удобно писать RTL-тесты - [CampaignMetrikaCounterEditorContainer.test.tsx](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna/src/containers/CampaignMetrikaCounterEditorContainer/CampaignMetrikaCounterEditorContainer.test.tsx)

# Создание тестов второго типа

1. Пишем в консоли `pnpm run storybook add`, отвечаем на 2 вопроса или запускаем команды из IDE [Webstorm]( #ide-config ) и [VScode]( #ide-vscode-config ).
2. Появляются файлы story.tsx и test.config.js
3. Удаляем из story.tsx лишнее, оставляем только `getComponent`
4. Удаляем `test.config.js`, если вам не нужен кастомный рендер (например, модалка рендерится не внутри .story-wrapper, поэтому ей надо указать кастомный метод `runCustomTest` — погуглите по проекту)
5. [Создаем типизированную фикстуру]( #typed-fixture ) или добавляем файл `fixture.js` следующего содержания:
```js
// Тут все поля из стора, которые вам нужны. Их можно сгенерировать через фикстуру, если их много (читайте доку выше)
export const fixture = {
    commonData: {
        isConversionMultipliersPopupEnabled: true
    }
}
```

6. Запускаем `npm run storybook test componentFolderPath`
7. На открывшемся `http://localhost:6060` убеждаемся, что все нормально
8. На открывшемся `http://localhost:8000` запускаем тест и акцептим скриншот
9. Можно коммитить

### Проблемы и решения:

#### Тест падает с ошибкой `Unexpected key $keyName found in previous state received by the reducer...`

Это означает, что в тесте не задан редьюсер для этого слайса стейта. Редьюсер можно задать в тесте в параметре `AddStory reducers` или в общем списке https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna/src/storybook/StoryBookDecorators/TestStoryProviderDecorator.tsx в getStoryRootReducer(). 

#### Как снять фикстуру с локально запущенного приложения?

`pnpm run storybook fixture [путь к тестовой стори (copy relative path в WS или VSCode)] -- --beta-port 3000`

Перед вызовом этой команды нужно запустить dna:

`pnpm run start`

Если dna не запущен, то команда `storybook fixture` попробует его запустить сама.

#### Долго ждать сборки для снятия фикстуры
Если нужный код уже есть на 8998.beta1.direct.yandex.ru (снимается фикстура для тестирования старого компонента), то фикстуру можно снять через 8998:

`pnpm run storybook fixture [путь к тестовой стори (copy relative path в WS или VSCode)] -- --beta-port 8998`

#### Если версия локального хрома не совпадает с нужной, то можно снять фикстуру удалённо
`pnpm run storybook fixture [путь к тестовой стори (copy relative path в WS или VSCode)] -- --remote`

#### Не создаётся туннель в Ubuntu по Windows
Если вы запускаете тесты из **Ubuntu по Windows**, то `tunneller` не сможет создать туннель.
![картинка](https://jing.yandex-team.ru/files/l-jul/ubuntu_ovdZi8bHDn.png)
Проблема в том, что в Ubuntu пользователь по-умолчанию будет `root`, с ним тунеллер не сможет соединиться по ssh.
Чтобы тунеллер использовал правильного пользователя – нужно запускать с переменной окружения `TUNNELER_USERNAME`:
```
TUNNELER_USERNAME=<твой доменный юзернейм> npm run storybook test
```

Чтобы каждый раз не писать `TUNNELER_USERNAME`, его можно добавить в `.bashrc`:
```
echo 'export TUNNELER_USERNAME=<твой доменный юзернейм>' >> ~/.bashrc
```
После добавления нужно перезагрузить терминал и запуск тестов должен работать без объявления TUNNELER_USERNAME при каждом вызове.

