## Команды для запуска автотестов
Для начала проект нужно собрать:

`./mvnw clean install -DskipTests -f pom.xml`

### Acceptance
`./mvnw clean test -Dtest=ru.yandex.autotests.mobile.disk.android.infrastructure.suites.FeatureSuite -Dcategories=Acceptance -f disk-tests/pom.xml`

### Business logic
`./mvnw clean test -Dtest=ru.yandex.autotests.mobile.disk.android.infrastructure.suites.FeatureSuite -Dcategories=BusinessLogic -f disk-tests/pom.xml`

### Regression
`./mvnw clean test -Dtest=ru.yandex.autotests.mobile.disk.android.infrastructure.suites.FeatureSuite -Dcategories=Regression -f disk-tests/pom.xml`

### Full regress
`./mvnw clean test -Dtest=ru.yandex.autotests.mobile.disk.android.infrastructure.suites.FeatureSuite -Dcategories=FullRegress -f disk-tests/pom.xml`

### Quarantine
`./mvnw clean test -Dtest=ru.yandex.autotests.mobile.disk.android.infrastructure.suites.FeatureSuite -Dcategories=Quarantine -f disk-tests/pom.xml`

### Уровни регресса можно комбинировать
`-Dcategories=Acceptance,BusinessLogic`

### Запуск на фичи
Чтобы запустить тесты на отдельные фичи, нужно добавить аргумент `features`, в котором указать фичи через запятую:

`-Dfeatures=Authorization,Delete files and folders,Aviary`

## Sandbox задачи

### Compilation
Таска для проверки компиляции автотестов. Запускается на каждый ПР.

https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_Disk_Android_MobileDiskClientAndroidIt_ArcDiskAndroidAutotestsCompilation?mode=builds

### Import
Таска для проставления флага isAutotest в Testpalm. Запускается каждый день по расписанию.

https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_Disk_Android_MobileDiskClientAndroidIt_ArcDiskAndroidAutotestsTestpalmImport?mode=builds

### Release
Таска для запуска всех автотестов на релизный билд. Запускается после отведения ветки ответственным за релиз. На самом деле запускает 4 отдельных job в teamcity

https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_Disk_Android_MobileDiskClientAndroidIt_DiskAndroidAutotestsRelease?mode=builds

### Tests

Конфиг для job, который запускают автотесты с указанием suite.

### Tests2

Конфиг для использования универсального FeatureSuite

