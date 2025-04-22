# Локализация в Java-проектах

Для локализации в java-проектах Директа нужно:

1. Создать класс, реализующий интерфейс [TranslationBundle](https://a.yandex-team.ru/arc_vcs/direct/libs/i18n/src/main/java/ru/yandex/direct/i18n/bundle/TranslationBundle.java) с ключами для русского текста.
2. Закоммитить его в `trunk`.
3. Дождаться пока скрипт [tanker.sh](https://a.yandex-team.ru/arc/trunk/arcadia/direct/bin/tanker.sh) загрузит ключи с русским текстом из созданного класса 
в [Tanker](https://tanker.yandex-team.ru/project/direct-java).
4. Подтвердить в Танкере русский текст и описать его контекст использования для каждого ключа (см. [Работа с Танкером](#work-with-tanker)).
5. [Создать тикеты](#create-translation-ticket) на перевод.
6. После того, как тикеты возьмут в работу и перевод будет готов, он приедет в `trunk` из Танкера в json-файлах и подцепится автоматически. 
Перевод из танкера привозит тот же скрипт tanker.sh, запускается [он каждые 4 часа](https://sandbox.yandex-team.ru/scheduler/11128/view)).

## Создание и использование класса, реализующего TranslationBundle

Создать класс можно по образу и подобию уже существующего класса, например, 
[CopyNamesTranslations](https://a.yandex-team.ru/arc_vcs/direct/core/src/main/java/ru/yandex/direct/core/copyentity/translations/CopyNamesTranslations.java?rev=r9046974#L8).

Получить локализованный текст можно, например, так:

```java
Translatable text = YourClassTranslations.INSTANCE.getSomeText();
String localizedText = translationService.translate(text, locale);
```

где translationService, это спринговый сервис [TranslationService](https://a.yandex-team.ru/arc_vcs/direct/common/src/main/java/ru/yandex/direct/common/TranslationService.java?rev=r8158820#L31), 
который можно получить как спринговый бин, или через `@Autowired` в любом проекте, зависящем от `direct/common`, а `locale` - это требуемая локаль класса `java.util.Locale`.

Если переводы из Танкера еще не приехали, вызов `translationService.translate(text, locale)` не упадет, а вернет текст в ближайшей локали, 
для которой перевод уже есть. Например, при отсутствии английского и украинского перевода, в английской и украинской локали вернется русский текст, 
а если есть английский перевод, то в турецкой локали вернется англиский, а в украинской - русский текст.

Чтобы новые ключи с русским текстом доехали до танкера (а перевод текста приехал обратно), нужно чтобы пакет класса `YourClassTranslations` 
был дочерним к пакетам, описанным в файле [tanker.sh](https://a.yandex-team.ru/arc/trunk/arcadia/direct/bin/tanker.sh?rev=r8710122#L64-73). 
Если невозможно сделать класс в пакете, дочернему к указанным в [tanker.sh](https://a.yandex-team.ru/arc/trunk/arcadia/direct/bin/tanker.sh?rev=r8710122#L64), 
нужно добавить желаемый пакет в `tanker.sh` и закоммитить его в `trunk`.

Сам скрипт запускается [средствами сэндбокса](https://sandbox.yandex-team.ru/scheduler/11128/view) раз в 4 часа.

После того как перевод будет готов, он приедет в виде json-файлов с именами `$ClassName.$lang.json` в папку `resources/locale/$package`, 
где `$ClassName` - имя класса, `$lang` - двухбуквенный код языка, а `$package` - пакет созданного класса. 
Например, для класса [CopyNamesTranslations](https://a.yandex-team.ru/arc_vcs/direct/core/src/main/java/ru/yandex/direct/core/copyentity/translations/CopyNamesTranslations.java?rev=r9046974#L8) 
переводы приедут [вот сюда](https://a.yandex-team.ru/arc_vcs/direct/core/src/main/resources/locale/ru/yandex/direct/core/copyentity/translations?rev=r9057784).

## Работа с Танкером { #work-with-tanker }

Все переводы для java-проектов Директа живут в Танкере в проекте [Direct-java](https://tanker.yandex-team.ru/project/direct-java). 
Заходим туда, и ищем в кейсетах свой класс, и кликаем в него (для примера будет использоваться 
[CopyNamesTranslations](https://a.yandex-team.ru/arc_vcs/direct/core/src/main/java/ru/yandex/direct/core/copyentity/translations/CopyNamesTranslations.java?rev=r9046974#L8)):

![no alt](_assets/tanker-find-class.png "Найти класс в Танкере")

Откроется окно со всеми ключами, требующими перевода:

![no alt](_assets/tanker-keys.png "Ключи в Танкере для перевода")

Нужно зайти в каждый ключ, подтвердить его русский текст, описать контекст его использования, и сохранить изменения:

![no alt](_assets/tanker-approve-text.png "Подтверждение русского текста в Танкере")

Всё, теперь можно создавать тикеты на перевод.

Если требуется, чтобы переводы появились до коммита локализуемого кода в `trunk`, нужно сначала создать в Танкере кейсет, с именем, как полное имя класса, 
реализующего интерфейс `TranslationBundle` (например, `ru.yandex.direct.core.copyentity.translations.CopyNamesTranslations`), создать тикеты на перевод, 
дождаться их выполнения, и только после этого коммитить локализуемый код в `trunk`.

## Создание тикетов не перевод { #create-translation-ticket }

Заходим на страницу [создания заказа](https://domains.yandex-team.ru/domain/loc/start/934?schemaId=3797) в службу локализации:

![no alt](_assets/tanker-add-ticket-1.png "Первая страница формы созания тикета на перевод")

Заполняем следующие поля:

- Тип задачи: Перевод.
- Вид текста: Интерфейс (или что-то другое из списка, наиболее подходщее по ситуации).
- Сущность танкера: ссылка на кейсет в танкере с нашим классом 
([пример](https://tanker.yandex-team.ru/project/direct-java/keyset/ru.yandex.direct.core.copyentity.translations.CopyNamesTranslations?branch=master&statuses=*%3D)).
- Языки: скорее всего это будут en-US, tr-TR и uk-UA. Полный список языков, используемых в Директе, 
можно [посмотреть тут](https://a.yandex-team.ru/arc_vcs/direct/libs/i18n/src/main/java/ru/yandex/direct/i18n/Language.java?#L13).

Скроллим форму вниз:

![no alt](_assets/tanker-add-ticket-2.png "Вторая страница формы созания тикета на перевод")

И заполняем следующие поля:

- ABC-Сервис: Директ.
- Название задачи: краткое название задачи.
- Описание задачи: краткое описание задачи, что за перевод нужно сделать и как он будет использоваться.
- Дедлайн: Обязательный параметр. Если сомневаешься какой указывать, спроси у менеджера или тимлида..
- Обоснование дедлайна: Плановый релиз.
- Связанные тикеты: твой тикет, в рамках которого потребовалась локализация.

Затем жмём на кнопку `Submit`.

Запустится процесс, и когда он закончится с зеленым статусом `Success`, к тебе на почту придет письмо о создании тикета на задачу локализации 
в очереди TRANSLATEADMIN ([пример тикета](https://st.yandex-team.ru/TRANSLATEADMIN-20292)).

Если потребуется, исполнители тебя в тикет призовут.

На этом всё.
