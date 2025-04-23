    # Тестопитек

[Обзорная статья](https://clubs.at.yandex-team.ru/mail/25713)

### Как настроить Тестопитек
- Получите любую роль в сервисе в [ABC](https://abc.yandex-team.ru/services/testopithecus/)
- Дальше см. readme в папке xmail

### Как проверить валидность модели и кросс-платформенных тестов
Для этого можно запустить все тесты в режиме "модель" против "модели"
Выбираем и запускаем конфигурацию `Run all tests on Model` из списка конфигураций справа сверху.
Тесты используют некоторые сервисы, доступы к которым должны прорасти через некоторое время после получения роли в ABC.
Если тесты прошли, то `nodejs` настроен.

### Как запустить тесты на бэкенд
Выбираем и запускаем конфигурацию `Run all tests on Mobile API` из списка справа сверху (см. `backend.ts`). 
Автотесты запустятся на случайном пользователе из пула. Его логин пароль будет в одной из первых строчек логов:
`Got account login=yandex-team-12993-09775 password=simple123456 uid=946220544`

### Абстракции 
Перед началом прочтите [обзорную статью](https://clubs.at.yandex-team.ru/mail/25713) про тестирование на основе модели.

В Тестопитеке ±5 абстракций:

- `Фича`  - некий кусок функциональности тестируемого приложения, представленный в Тестопитеке произвольным интерфейсом

Пример: фича поворота экрана
```typescript
export interface Rotatable {
  isInLandscape(): boolean

  rotateToLandscape(): void

  rotateToPortrait(): void
}
```
- `Компонент` (`MBTComponent`) - экран тестируемого приложения. Определяет то, что нужно считывать с экрана и как это сверять с моделью.

Пример: компонент списка писем 
```typescript
export class MaillistComponent implements MBTComponent {
  public assertMatches(model: App, application: App): void {
      ...
  }
}
```

- `Действие` (`MBTAction`) - обертка над вызовом методов `фичи`, меняющих состояние приложения. Действие может переводить приложение из одного `компонента` в другой.

Пример: открываем компоуз из списка писем
```typescript
export class OpenComposeAction extends WriteMessageBaseAction {
  public performImpl(modelOrApplication: WriteMessage, currentComponent: MBTComponent): MBTComponent {
    modelOrApplication.openCompose()
    return new ComposeComponent()
  }
}
```
- `Тест` (`MBTTest`) - последовательность `действий`, между которыми при запуске вызывается `assertMatches` у соответствуующих `компонент`. 
Кроме того, тест должен говорить, как должен быть наполнен почтовый ящик перед запуском 

Пример: 
```typescript
export class MoveToSpamFirstMessageTest extends RegularYandexTestBase {
  constructor() {
    super('first message should be deleted from inbox if move to spam')
  }

  public prepareMailbox(mailbox: ImapMailboxBuilder): void {
    mailbox
      .nextMessage('subj')
      .nextMessage('subj2')
  }

  public regularScenario(account: UserAccount): TestPlan {
    return TestPlan.yandexLogin(account)
      .then(new MoveToSpamAction(0))
      .then(new MoveToSpamAction(0))
  }
}
```

Каждая `фича` реализуется в идеально работающей простой `кросс-платформенной модели` и в `тестируемом приложении`

- `Модель` (`MailboxModel`) - реализация `фичей` в виде сильно упрощенной почты без GUI, многопоточности, базы данных и т.п.

Пример: модельная реализация поворота экрана
```typescript
export class RotatableModel implements Rotatable {
  public landscape: boolean = false
  
  public isInLandscape(): boolean {
    return this.landscape;
  }

  public rotateToLandscape(): void {
    this.landscape = true
  }

  public rotateToPortrait(): void {
    this.landscape = false
  }
}
```
- В `тестируемом приложении` `фича` реализуется через вызов селекторов для конкретного приложения (iOS/Android).
Пример реализации `фичи` `Rotatable` для Android-автотестов:
```
class RotatableApplication(driver: AndroidDriver<WebElement>): Rotatable {
    private val commonUserSteps = CommonUserSteps(driver)

    override fun isInLandscape(): Boolean {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

    override fun rotateToLandscape() {
        commonUserSteps.rotateDevice(ScreenOrientation.LANDSCAPE)
    }

    override fun rotateToPortrait() {
        commonUserSteps.rotateDevice(ScreenOrientation.PORTRAIT)
    }
}
```
После этого становится возможным проверить работу приложения по модели. 
Кросс-платформенный код `фичей`, `модели`, `компонент` и `тестов` транслируется в ваши автотесты, к ним добавляется реализация фичей через селекторы в ваших автотестах.
В результате становится возможным запустить тест на вашей платформе (см. `Как запустить один кросс-платформенный тест`).


### Где что лежит

Для того, чтобы протестировать новую функциональность надо добавить фичу, реализовать ее в модели и в приложении, 
сделать действия и составить из них несколько кросс-платформенных тестов.
`Фича` - некий кусок функциональности тестируемого приложения, представленный в Тестопитеке произвольным интерфейсом. Примеры фичей живут `mail-features.ts`.
У каждой фичи есть ее метаинформация (имя и пр.) - наследник класса `Feature`.
Для того, чтобы ваша функциональность могла быть протестирована, соответсвующая фича должна быть реализована и в модели, и в приложении.
Реализация фичи в модели добавляется через класс `MailboxModel` (там много примеров).
Реализация фичи в приложении добавляется в проекте ваших автотестов - через класс `MobileMailBackend` для мобильного API, `AndroidMailboxApplication.kt` для Android и `IOSMailboxApplication.swift` для iOS.
Методы фичи, которые меняют состояние приложения, следует завернуть в `Действия` (`MBTAction`).
Действие переводит приложение из одного компонента в другой компонент (`MBTComponent`) после выполнения метода `perform`.
По сути, компонент - это один из экранов приложения.
Все проверки записываются в `assertMatches` у соответствующего компонента. Проверки должны использовать read-only методы вашей фичи.
Для каждого мутабельного метода вашей фичи надо сделать наследника `MBTAction`. В папке `actions` есть много примеров. 
Дальше можно написать кросс-платформенный тест, который протестирует вашу функциональность (см. папку `tests`).
Каждый тест - это просто последовательность action-ов. Платформа сама будет вызывать `assertMatches` между действиями при прогоне теста.

#### Чтобы протестировать вашу функциональность надо:
- Добавить фичу в `mail-features.ts`
- Добавить ее реализацию в `MailboxModel` - прописать в `allSupportedFeatures` и в `getFeature`
- Если надо, написать новый компонент `MBTComponent`
- Создать несолько `MBTAction` для действий в вашей функциональности
- Написать несколько `MBTTest`-ов при помощи новых `MBTAction`-ов
- Запустить проверку их валидности - конфигурацию `Run all tests on Model`
- Странслировать полученный код в ваши автотесты (см. соответствующие разделы ридми)
- Реализовать и зарегестрировать фичу уже в автотестах для интересующей платформы - прописать ее в `supportedFeatures` 
и в `getFeature` в `AndroidMailboxApplication.kt` для Android и `IOSMailboxApplication.swift` для iOS 
- Позапускать свои тесты (см. `Как запустить один кросс-платформенный тест`)

Такой подход позволяет автоматически генерировать автотесты для вашей функциональности.
Платформа сама это сделает. Кроме того, она сгенерирует так называемый "умный обход", который протестирует все возможные состояния вашей фичи. 


### Как написать кросс-платформенный тест
Если у вас обычный тест, который использует один яндексовый аккаунт, то надо в папке `code/tests` 
реализовать класс-наследник `RegularYandexTestBase`. Там много подобных примеров.
Если ваш тест более сложный, то надо отнаследоваться от `AbstractMBTTest` 
Если у вашего теста есть братишка в Пальме, то вы можете переопределить метод `testSettings` - он должен вернуть конфиг с id соответсвующих кейсов.
Пример такого теста - `InboxTopBarDisplayTest` из `inbox-top-bar-display-test.ts`
Реализованный тест следует зарегистрировать в `register-your-test-here.ts`

### Как запустить один кросс-платформенный тест
Все тесты регистрируются в `register-your-test-here.ts` и на каждой платформе запускаются всем скопом под одним параметризированным тестом
(см. `TestopithecusFixedScenarioTests.swift / TestopithecusFixedScenarioTests.kt / backend.ts`).
Для запуска одного теста раскомментируйте строку с `TestsRegistry.testToDebug` и в качестве значения укажите свой тест.
После чего запустите конфигурацию с тестопитековскими тестами (`Run Testopithecus Tests` в Android, 
`TestopithecusFixedScenarioTests [Debug]` в iOS и `Run all tests on Mobile API` для бэкенда)

### Как сгенерировать код для автотестов (2 варианта)
1. Выполняем `Generate: I changed only testopithecus`
2. Либо коммитим исходный сходный .ts код в групповую ветку `arc push -u groups/...`
После чего запускаем билд [IntegrateXPlat](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=MobileNew_Monorepo_Mail_Common_XMailIntegrateXPlat) 
на этой ветке. Сгенерированные файлы приедут в ветку

### Как сделать пул-реквест в Testopithecus
- Коммитим и пушим все новые и изменившиеся файлы (в т.ч. на swift)
- Важно: убеждаемся, что во вкладке снизу `Arc` в разделе `Unversioned Files` нет незакоммиченных файлов с исходным кодом
- Делаем пул реквест https://wiki.yandex-team.ru/mobvteam/arc-macos/#branchi 
- Добавляем в ревьюеры `a-zoshchuk`
- После прохождения ревью включаем автомерж через нажатие на `Merge` -> `Enable automatic merging` на странице пул реквеста

### Как получить OAuth токен пользователя по логину-паролю
OAuth токен можно получить, выполнив такой запрос 
```
curl -v -F grant_type=password -F username=LOGIN -F password=PASSWORD -F client_id=e7618c5efed842be839cc9a580be94aa -F client_secret=81a97a4e05094a4c96e9f5fa0b21f794 "https://oauth.yandex.ru/token"
```

### Как нарисовать граф
- Запускаем `Print model graph`, после выполнения должен появиться файл `graph.txt`
- В консоли выполняем команду `dot -ofile -O -Tpng graph.txt`, после выполнения должен появиться файл `graph.txt.png`
- PROFIT

### Как запустить тесты на кастомный бэкенд Почты
Некотороые автотесты в тестопитеке умеют тестировать и почтовый бэкенд. Правда, пока только для яндексовых аккаунтов.
- Открываем кофигурацию в Тимсити https://teamcity.yandex-team.ru/viewType.html?buildTypeId=MobileNew_Monorepo_Mail_Common_MailCommonTestopithecusTestMobileMailBackend
- Нажимаем `Run`
- Выбираем хост мобильного API, который смотрит в тестируемый бэкенд.
- Запускаем
Это ровно те тесты, которые тестируют UI наших приложений, только при тестировании бэкенда они не кликают в экран, а дергают ручки бэкенда.
В отличае от обычных тестов на бэкенд, эти тесты проверяют сложные сценарии, которые соответствуют сценариям в приложении.
За счет этого они гораздо более эффективные и могут найти проблемы, которые обычные тесты не найдут.
Важно: мы пока умеем брать аккаунты только из прод. паспорта, поэтому ваш бэк должен смотреть в прод паспорт.

### Как запустить тесты на бэкенд внешних почт
Если у вас есть аккаунт внешней почты, который можно сносить, и на котором вы хотите протестировать XENO, 
то для запуска тестов надо сделать следующее
- Залогиниться в приложении iOS/Android интересующим аккаунтом
- Подсмотреть в сниффере OAuth токен пользователя
- Вставить его в OauthService вместо ***
- Пойти в класс UserServiceEnsemble и отредактировать метод getDebugAccount
- Надо в switch написать ваш аккаунт с его типом (в качестве примера там есть mail)
- Найти класс RegularYandexTestBase и поменять там requiredAccounts на тот тип аккаунта, который вы тестируете
- Все, теперь можно запускать конфигурацию `Run all tests on Mobile API`
- Она будет долго идти, поскольку перед каждым тестом мы будем ждать, пока XENO засинкает аккаунт внешней почты
- В логах после строчки `Model vs Application testing started` можно смотреть за тестированием бэка
- Все запросы, которые мы посылаем, отображаются в формате curl
- Все действия, которые мы делаем, описываются после слов `Performing action`
- После каждого действия мы скачиваем текущий ящик (его состояния) и рисуем в ASCII-арте его вместе с ящиком модели после слов `DEBUG DUMP`
- Список всех ручек, которые мы дергаем, есть тут https://wiki.yandex-team.ru/users/jkennedy/apimobile/

Найденные проблемы:
1) Пометка письма прочитанным/непрочитанным сразу не применяется, то есть после следующего запроса 
данные о письме прилетают с старом состоянии. Из-за этого падает ряд тестов, которые помечают письмо прочитанным

### Как запустить тесты на Desktop
- Скачиваем устаналиваем Desktop приложение https://desktop.s3.mdst.yandex.net/Yandex.Mail-1.3.28.dmg 
Оно должно появиться по пути `/Applications/Yandex.Mail.app/Contents/MacOS/Yandex.Mail`
- Открываем его и залогиниваемся один раз. Приложение захочет обновиться - соглашаемся.
- Идем в `desktop-tests.ts`
- Убираем .skip
- Запускаем конфигуарцию `Run all tests on Desktop`

### Как создать тестовых пользователей в [TUS](https://wiki.yandex-team.ru/test-user-service/)
- Получаем [OAuth-токен](https://wiki.yandex-team.ru/test-user-service/#autentifikacija)
- Вызываем скрипт `./create_tus_users.sh <your token here>`
- Скрипт создает по 20 пользователей в захардкоженых тегах

### Как починить самоподписанный сертификат yandex-team
Для nodejs/модельных тестов:
Сертификат лежит в `testopithecus/YandexInternalRootCA.crt`. Для того, чтобы он подхватился, нужно в конфигурации
запуска добавить переменную окружения `NODE_EXTRA_CA_CERTS`, в которой передать путь к файлу 
(см. конфигурацию "Run all tests on Model").

### Публикации
https://clubs.at.yandex-team.ru/mail/25713
https://clubs.at.yandex-team.ru/mail/25718
https://clubs.at.yandex-team.ru/mail/26290

### Сторонние Аккаунты для Тестирования Почты

При необходимости тестирования в тестопитеке аккаунтов других сервисов, их данные:

####Yahoo:

Name: testovian@yahoo.com

Password: yandexovian1

UID: 10004780412

####Mail.ru:
Name: testovian@mail.ru

Password: yandexovian2

UID: 1000135477

####Outlook: 
Name: testovian@outlook.com
Password: yandexovian3
UID: 1000422216
