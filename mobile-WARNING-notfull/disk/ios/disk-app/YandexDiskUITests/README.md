# UI автотесты Мобильного Диска для iOS

## Предусловия
### Файлы конфигурации для запуска из Xcode
Для запуска автотестов локально нужно создать файл test.properties в директории YandexDiskUITests со следующим содержимым:
```
use.new.account.management=true
tus.url=https://tus.yandex-team.ru
tus.token=TOKEN // ссылка для получения токена - https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9052de6e4cf142039a7ee44ac03e4614
tus.consumer=mobdisk
tus.default.tags=common
tus.lock.duration=600
app.client.id=<Test application client id>
app.client.secret=<Test application client secret>
```
### Тестовое приложение для OAuth
Для запуска автотестов нужно специальное тестовое приложение. Его секреты можно забрать из [Секретницы](https://yav.yandex-team.ru/secret/sec-01d1rj50w2fbvsrzkq09n12dre/explore/versions).
У приложения выставлены следующие доступы в OAuth:
```
cloud_api:disk.app_folder,cloud_api:disk.read,cloud_api:disk.write
```
Кроме того, у него выставлен grant type в password, что позволяет упростить процесс получения токенов.

### Пользователи, используемые в тестах.
Пользователи используемые в автотестах должны соответствовать паттерную `yndx-*` или `yandex-team-*`.
Это необходимо для работы QA ручек. Таких пользователей можно создать **только внутри сети Яндекса**.
Мы переехали на использование пула пользователей, поэтому в большинстве кейсов нет никакой необходимости в ручном создании пользователей для автотестов.


## Запуск имеющихся тестов

### Запуск из Xcode
1. [Нужно настроить и собрать проект](../README.md).
2. Выбрать схему `YandexDiskUITests` для запуска.
3. Выбрать симулятор. Тесты на данный момент расчитаны на iPhone 8 и iPad Air. На симуляторе должен быть выбран английский язык.
4. Выбрать тест для запуска в Test Navigator или из кода и запустить его.

## Запуск из консоли отдельных тестов
1. [Нужно настроить и собрать проект](../README.md).
2. Собрать тесты: `xcodebuild -workspace "YandexDisk.xcworkspace" -scheme "YandexDiskUITests"  -configuration "Debug" -destination "platform=iOS Simulator,name=iPhone 7,OS=12.2" -derivedDataPath "./build" clean build-for-testing`
3. Запустить собранные тесты: `xcodebuild -workspace "YandexDisk.xcworkspace" -scheme "YandexDiskUITests"  -configuration "Debug" -destination "platform=iOS Simulator,name=iPhone 7,OS=12.2" -derivedDataPath "./build" test-without-building -only-testing:YandexDiskUITests/AcceptanceCopyFilesTestsiPhone`

### Запуск из консоли через скрипт
1. [Нужно настроить и собрать проект](../README.md).
2. Определить при необходимости переменную окружения TARGET_DEVICE_TYPE. Возможные значения: iPhone или iPad.
3. Определить при необходимости переменную TEST_PRIORITY. Возможные значения Acceptance, BL, Regression.
4. Задать переменную окружения XCODE_VERSION, что бы она указывала на Xcode по умолчанию: `export XCODE_VERSION=Xcode`
5. Запустить скрипт `./generateTestList.sh`
6. Запустить автотесты через FastLane. Например: `./fastbuild_repo/common/tools/fastbuild/fastlane.sh ui_tests xcodeApp:"Xcode.app" testDevice:"iPhone 7" testOSName:"iOS" testOSVersion:"13.2.2"`
7. Запустить сборку Allure отчета скриптом `./buildReport.sh`. Сгенерированный отчет будет лежать в директории allure-report в корне проекта.
8. При необходимости импортировать ран в Testpalm при помощи importRun.sh

### Импорт ранов в Testpalm
*Скорее всего, это не стоит делать*
1. Определить переменную окружения TESTPALM_TOKEN, указав токен пользователя, от имени которого будут импортироваться результаты.
2. Определить переменную окружения TESTPALM_PROJECT, указав проект, в который будут импортироваться раны. В нашем случае idisk.
3. Определить при необходимости переменную окружения TESTPALM_VERSION.
4. Определить при необходимости переменную окружения TESTPALM_SUITE.
5. Убедиться, что есть собранный Allure отчет в корне проекта.
6. Запустить импортер `./importRun.sh testpalm_run_name`


## Аккаунты используемые в тестах
Про Test User Service - https://wiki.yandex-team.ru/test-user-service/

### tags: "idisk-2272" - аккаунты с папкой TestDir с 8 файлами и соответственным контентным блоком в корне раздела Лента с кнопкой "Посмотреть все"

1. login - yndx-autotest-idisk-2272-1, uid - 1022898564

### tags: "idisk-1442" - аккаунты с папкой  TestDir, в которой 3 папки и 6 файлов для проверки порядка сортировки

1. login - yndx-autotest-idisk-1442-1, uid - 1027499388
2. login - yndx-autotest-idisk-1442-2, uid - 1027637853

### tags: "idisk-4223" - пустые аккаунты

1. yndx-autotest-ios-idisk-4223-1, uid - 1575966784
2. yndx-autotest-ios-idisk-4223-2, uid - 1575966541

### tags: "idisk-2273" - аккаунты с одним фото в разделе Фото для проверки тапбара в ГО

1. login - yndx-autotest-idisk-2273, uid - 1038684597
2. login - yndx-autotest-idisk-2273-2, uid - 1039961375

### tags: "idisk-5363" - аккаунты с 4 файлами(docx, xlsx, txt, pdf) в папке Docs и одним контентным блоком в ленте для проверки открытия этих файлов

1. login - "yndx-autotest-idisk-5363-1", uid - 1056756222

### tags: "idisk-5084" - аккаунт с одним блоком фотоподборок с заголовком "Photos of the month" и подзаголовком "September 2019"

1. login - "yndx-autotest-idisk-5084-1", uid - 1058993211

### tags: “idisk-content-blocks" - в аккаунте 3 контентных блока с 1, 5, 9 файлами в папках 1_file, 5_photos, 9_photos соответственно

1. BANNED login - yndx-autotest-idisk-cb-1, uid - 1059042715
2. BANNED login - yndx-autotest-idisk-cb-2, uid - 1059048672
3. yndx-autotest-idisk-cb-3, uid - 1576000809
4. yndx-autotest-idisk-cb-4, uid - 1576001613

### tags: "idisk-5617" - в аккаунте один персональный альбом "PreparedAlbum" с одной фото "Bears.jpg" внутри

1. yndx-autotest-ios-idisk-5617-1, uid - 1575873842
2. yndx-autotest-ios-idisk-5617-2, uid - 1575873498

### tags: "idisk-2269" - в аккаунт загружено одно фото "jolie.jpg" для не пустого фотосреза

1. yndx-autotest-ios-idisk-2269-1, uid - 1575895304
2. yndx-autotest-ios-idisk-2269-2, uid - 1575895514

### tags: “idisk-social-blocks" - в аккаунте 3 социальных блока с 1, 5, 9 файлами

1. login - yndx-autotest-idisk-sb-1, uid - 1059055279
2. login - yndx-autotest-idisk-sb-2, uid - 1059060140

### tags: “idisk-autoupload-blocks" - в аккаунте 3 безлимитных блока с 1, 4, 9 файлами

1. login - yndx-autotest-idisk-ab-1, uid - 1059042715
1. login - yndx-autotest-idisk-ab-2, uid - 1059068434

### tags: “idisk-common-autoupload-blocks" - в аккаунте контентные блоки и блоки обычной автозагрузки

1. login - yndx-autotest-idisk-cab-1, uid - 1155636266
1. login - yndx-autotest-idisk-cab-2, uid - 1155636891

### tags: “idisk-all-albums" - в аккаунте есть все существующие альбомы (Избраные, Камера, Видео, Скриншоты, Красивые, Разобрать, Личный - “Cats")

1. BANNED login - yndx-autotest-idisk-albums-1, uid - 1061479223
2. BANNED login - yndx-autotest-idisk-albums-2, uid - 1061479398
3. BANNED login - yndx-autotest-idisk-albums-3, uid - 1063757941
4. BANNED login - yndx-autotest-idisk-albums-4, uid - 1063758188
5. login - yndx-autotest-idisk-albums-5, uid - 1580910355
6. login - yndx-autotest-idisk-albums-6, uid - 1581185005
7. login - yndx-autotest-idisk-albums-7, uid - 1581195039
8. login - yndx-autotest-idisk-albums-8, uid - 1581196568

### tags: “idisk-5742" - в аккаунтах дефолтные файлы, файл Mountains.jpg добавлен в альбом "Избранные"

1. yndx-autotest-idisk-5742-1, uid - 1580560839
1. yndx-autotest-idisk-5742-2, uid - 1580562733

### tags: “geoalbums" - аккаунт с гео альбомами, используется в одноименных автотестах, для проверок без изменения контента

1. login - yandex-team-80167-72354, uid - 1057532239

### tags: "idisk-5806" - пустые аккаунты

1. yndx-autotest-ios-idisk-5806-1, uid - 1575205426
2. yndx-autotest-ios-idisk-5806-2, uid - 1575205673

### tags: “idisk-special-geo-albums" - на аккаунте один гео альбом для проверки перемещения/переименования внутри гео альбома, используются только в тестах idisk-5239 и idisk-5241

1. login - yndx-autotest-idisk-geosp-1, uid - 1100016002
2. login - yndx-autotest-idisk-geosp-2, uid - 1100016075

### tags: "idisk-5912" - на аккаунте три фото (от 12 июня, 17 июня и 27 мая) для проверки склеивания моментов в ваусетке фотосреза

1. login - yndx-autotest-idisk-5912-1, uid - 1116647088

### tags: "idisk-4422" - на аккаунте одно фото, для проверки обновления рекламы после закрытия просмотрщика в разделе Файлы

1. login - yndx-autotest-idisk-4422, uid - 1118936867

### tags: "idisk-5515" - на аккаунте две папки с фото, для проверки обновления рекламы после перехода по папкам

1. login - yndx-autotest-idisk-5515, uid - 1125289433

### tags: "idisk-4315_5969" - на аккаунтах одно безлимитное фото в разделе Фото, для проверок в тестах 4315 и 5969

1. login - yndx-autotest-idisk-43155969, uid - 1165408001
2. login - yndx-autotest-idisk-431559692, uid - 1165408920

### tags: "idisk-viewerinfo" - на аккаунтах одно фото для проверки инфопанели в просмотрщике, в тестах idisk-4342 и idisk-4343

1. login - yndx-autotest-idisk-info-1, uid - 1165274406
2. login - yndx-autotest-idisk-info-2, uid - 1165274571

### tags: "idisk-4359" - на аккаунтах в ленте 5 фотоподборок, используются одноименном тесте, для проверок без изменения контента

1. login - yndx-autotest-idisk-4359-1, uid - 1199022090
2. login - yndx-autotest-idisk-4359-2, uid - 1199022384

### tags: "idisk-4986" - на аккаунтах 2 блока с фото, в одном больше 8 файлов, в другом меньше, используются в тестах idisk-4986 и idisk-5778

1. login - yndx-autotest-idisk-4986-1, uid - 1199728765
2. login - yndx-autotest-idisk-4986-2, uid - 1199729185

### tags: "persalbums" - на аккаунтах 2 фото - в папке фотокамера (photo.jpg) и в корне раздела Файлы (photo1.jpg), обе отображаются в фотосрезе. Аккаунты используются в тестах BLPersonalAlbumsChangesTests

1. login - yndx-autotest-persalbums-1, uid - 1218471072
2. login - yndx-autotest-persalbums-2, uid - 1218481411

### tags: "idisk-1004" - на аккаунтах используются 6 фото и 1 папка - 2 дефолтных (Bears.jpg, Mountains.jpg) и одно уникальное (pngImage.png) в корне раздела Файлы и папка  TestDir, в которой 3 фото файла  для добавления в Офлайн

1. login - yndx-autotest-idisk-1004-1, uid - 1506176658
2. login - yndx-autotest-idisk-1004-2, uid - 1506176200

### tags: "idisk-1533" - на аккаунтах 2 папки: расшаринная папка "FA Dir" c фото (pngImage.png), папка  Camera Uploads с фото (photo1.jpg) и фото в корне раздела Файлы (photo.jpg). 

1. yndx-autotest-idisk-1533-1, uid - 1507009220
2. yndx-autotest-idisk-1533-2, uid - 1507010699

### tags: "idisk-4399" - аккаунты с одним фото в альбоме "красивые"

1. yndx-autotest-idisk-4399-1, uid - 1571008113
2. yndx-autotest-idisk-4399-2, uid - 1571008247

### tags: "idisk-3218" - аккаунты с двумя фото в фотосрезе

1. yndx-autotest-idisk-3218-1, uid - 1580878799
2. yndx-autotest-idisk-3218-2, uid - 1580879787

### tags: "idisk-1945" - аккаунты с одним фото "Cat_1.HEIC" в фотосрезе

1. yndx-autotest-idisk-1945-1, uid - 1581203603
2. yndx-autotest-idisk-1945-2, uid - 1581205885

### tags: "idisk-1533-folderFA" -  Аккаунт yndx-autotest-idisk-1533fa является хранилищем папки "FA Dir" которая поделена на других пользователей (c тегом idisk-1533) с правами Full Access

1. yndx-autotest-idisk-1533fa, uid - 1513129810

### tags: "idisk-5851" - аккаунты с одним контентным блоком с одним медиафайлом

1. yndx-autotest-ios-idisk-5851-1, uid - 1575269828
2. yndx-autotest-ios-idisk-5851-2, uid - 1575269929

### tags: "idisk-6229" - аккаунты с 28 файлами для тестирования множественного выбора

1. yndx-autotest-idisk-6229-1, uid - 1566368837
2. yndx-autotest-idisk-6229-2, uid - 1566375668

### tags: "idisk-2399" - Аккаунты с дефолтными файлами

1. BANNED yndx-autotest-idisk-2399-1, uid - 1562697003
2. BANNED yndx-autotest-idisk-2399-2, uid - 1562697133
3. yndx-autotest-idisk-2399-3, uid - 1580550806
4. yndx-autotest-idisk-2399-4, uid - 1580552268

### tags: "idisk-5812" - Аккаунты с дефолтными файлами

1. yndx-autotest-idisk-5812-1, uid - 1577312829
2. yndx-autotest-idisk-5812-2, uid - 1577312665

### tags: "idisk-6167" - аккаунты с одной заметкой с заголовком "Note for idisk-6167"

1. BANNED yndx-autotest-idisk-6167-1, uid - 1570965630
2. BANNED yndx-autotest-idisk-6167-2, uid - 1570965834
3. yndx-autotest-idisk-6167-3, uid - 1580553438
4. yndx-autotest-idisk-6167-4, uid - 1580554923

### tags: "ios-shared-dir-cases" - аккаунты с именем "Share Main"

1. yndx-autotest-ios-share-1, uid - 1574505051
2. yndx-autotest-ios-share-2, uid - 1574505198
3. yndx-autotest-ios-share-3, uid - 1574505277
4. yndx-autotest-ios-share-4, uid - 1574505346
5. yndx-autotest-ios-share-5, uid - 1574505441
6. yndx-autotest-ios-share-6, uid - 1574505491
7. yndx-autotest-ios-share-7, uid - 1574505551
8. yndx-autotest-ios-share-8, uid - 1574505611

### tags: "idisk-6267" - аккаунты с дефолтными файлами

1. yndx-autotest-idisk-6267-1, uid - 1572833134
2. yndx-autotest-idisk-6267-2, uid - 1572833034

### tags: "idisk-3293" - аккаунты для изменения настроек нотификаций во время теста

1. yndx-autotest-idisk-3293-1, uid - 1576690125
2. yndx-autotest-idisk-3293-2, uid - 1576689138

### tags: "idisk-3293-2" - аккаунты у которых включены все нотификации, кроме "Other"

1. yndx-autotest-idisk-3293-2-1, uid - 1576690446
2. yndx-autotest-idisk-3293-2-2, uid - 1576690937

### tags: "idisk-4269" - аккаунты с одним блоком "Photo uploaded" в ленте

1. yndx-autotest-idisk-4269-1, uid - 1583829864
2. yndx-autotest-idisk-4269-2, uid - 1583836942

### tags: "idisk-2279" - аккаунты у которых загружен большой текстовый файл "big_text_file.txt"

1. yndx-autotest-idisk-2279-1, uid - 1583252898
2. yndx-autotest-idisk-2279-2, uid - 1584760948


### tags: "idisk-3398" - аккаунты с двумя фото в фотосрезе. Лежат в папке test. Первое фото с именем "1.JPG"

1. yndx-autotest-idisk-3398-1, uid - 1585281749
2. yndx-autotest-idisk-3398-2, uid - 1585290793

### tags: "idisk-976" -  На аккаунтах лежит большой файл "bigVideo.mov" для его загрузки в офлайн

1. yndx-autotest-idisk-976-1, uid - 1585371458
2. yndx-autotest-idisk-976-2, uid - 1585374702


### tags: "idisk-2985" -  Пустые аккаунты

1. yndx-autotest-idisk-2985-1, uid - 1626215657
2. yndx-autotest-idisk-2985-2, uid - 1626216039

### tags: "idisk-1469" - Пустые аккаунты

1. yndx-autotest-idisk-1469-1, uid - 1631820906
2. yndx-autotest-idisk-1469-2, uid - 1631821154

### tags: idisk-4775 - Пустые аккаунты для автозагрузки фото по кейсу

1. yndx-autotest-idisk-4775-1, uid - 1632664567
2. yndx-autotest-idisk-4775-2, uid - 1632664757

### tags: idisk-4728 - Пустые аккаунты для автозагрузки фото и видео по кейсу

1. yndx-autotest-idisk-4728, uid - 1644693726
2. yndx-autotest-idisk-4728-1, uid - 1644695471

### tags: idisk-2818 - Пустые аккаунты для безлимитной автозагрузки фото по кейсу

1. yndx-autotest-idisk-2818-1, uid - 1644872468
2. yndx-autotest-idisk-2818-2, uid - 1644873202

### tags: "idisk-1943" - Пустые аккаунты

1. yndx-autotest-idisk-1943-1, uid - 1650576847
2. yndx-autotest-idisk-1943-2, uid - 1650577402

### tags: "idisk-4380" - Аккаунты с дефотными файлами
yndx-autotest-idisk-4380-1, uid - 1660444143 
yndx-autotest-idisk-4380-2, uid - 1660444493

### tags: "idisk-3364" - аккаунты с одним файлом "generated"
1. yndx-autotest-idisk-3364-1, uid - 1656162723
2. yndx-autotest-idisk-3364-2, uid - 1656162876

### tags: "idisk-2691" - пустые аккаунты
yndx-autotest-idisk-2691-1, uid - 1656441831
yndx-autotest-idisk-2691-2, uid - 1656442120

### tags: "idisk-2709" - дефолтные аккаунты
yndx-autotest-idisk-2709-1, uid - 1656627296
yndx-autotest-idisk-2709-2, uid - 1656627761

### tags: "idisk-2892" - аккаунты с одним файлом "simpleFile"
yndx-autotest-idisk-2892-1, uid - 1657327497
yndx-autotest-idisk-2892-2, uid - 1657327789

### tags: "idisk-5172" - аккаунты c дефолтными файлами
yndx-autotest-idisk-5172-1, uid - 1657570221
yndx-autotest-idisk-5172-2, uid - 1657571588

### tags: "idisk-2885" - аккаунты с одним файлом pngImage.png в папке TestDir
yndx-autotest-idisk-2885-1, uid - 1657726056
yndx-autotest-idisk-2885-2, uid - 1657727057

### tags: "idisk-2885-share" - аккаунты с дефолтными файлами
yndx-test-idisk-2885-share-1, uid - 1657727685
yndx-test-idisk-2885-share-2, uid - 1657727883

### tags: "idisk-2893" - аккаунты с одним файлом "generated.txt"
yndx-autotest-idisk-2893-1, uid - 1658978250
yndx-autotest-idisk-2893-2, uid - 1658978407

### tags: "idisk-2887" - аккаунты с одним файлом "pngImage.png"
yndx-autotest-idisk-2887-1, uid - 1659161098
yndx-autotest-idisk-2887-2, uid - 1659161368

### tags: "idisk-5536" - Аккаунты с дефолтными файлами у которых нет истории. Они считаются новыми и после закрытия онбординга отрывается раздел файлов.
yndx-autotest-idisk-5536-1, uid - 1660621403
yndx-autotest-idisk-5536-2, uid - 1660623182

### tags: "idisk-5602" - пустые аккаунты
yndx-autotest-idisk-5602-1, uid - 1660997815
yndx-autotest-idisk-5602-2, uid - 1660997982
