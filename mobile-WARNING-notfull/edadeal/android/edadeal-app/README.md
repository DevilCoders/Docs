# Основные понятия
- **Retailer** - сеть магазинов (Перекресток, Билла)
- **RetailerType** - тип сети (супермаркет, детский, косметика)
- **Shop** - конкретный магазин сети
- **Offer (Product/Item)** - конкретный товар
- **Catalog** - список Offer'ов (аналог бумажного каталога)
- **Segment (Category/SubCategory)** - категория (сегмент) товара (Молоко, Мясо, Продукты),
    может иметь родительский Segment. У товара может быть только 1 сегмент.
- **Compilation** - подборка товаров (Лучшие предложения, Молоко, Детское питание),
    может иметь родительскую Compilation. Товар кожет быть в нескольких подборках.
- **SubSegment/SubCompilation** - сегмент/подборка 2го уровня (имеет 1 родителя)
- **RootSegment/RootCompilation** - сегмент/подборка 1го уровня
- **QuantityUnit** - тип количества товара (л, кг)
- **DiscountUnit** - тип скидки (%, руб)
- **Cart (Basket)** - список покупок

# Модули проекта
- **app** - основной модуль приложения
- **emp-config, emp-webapp** - модули для [взаимодействия](https://wiki.yandex-team.ru/edadeal/architecture/webview-native-interaction/) с [вебаппами](https://wiki.yandex-team.ru/edadeal/architecture/webapps/)
- **moshi-ext** - утилиты для работы с Moshi
- **okhttp-cache-ext** - fork реализации кэширования для OkHttp с поддержкой дополнительных директив
- **ktor** - fork ktor'a, используется как локальный http и [ws сервер](https://wiki.yandex-team.ru/edadeal/architecture/webapps/test-experiment/) для взаимодействия с вебаппами

# Основные классы приложения
- **data/..** - логика для работы с данными: репозитории, база, работа с файлами, миграции
- **di/...** - инициализация компонентов приложения. Сейчас используется service locator(Module), планировали рассмотреть переход на полноценный DI(Dagger2, Toothpick)
- **dto/...** - структуры данных, приходящих из API в формате json
- **model/api/...** - авторизационное(UsrApi), рекламное(AdsApi), chercher(SearchApi) и другие API
- **data/Repository** - хранилище данных (ритейлеры, сегменты, офферы)
- **data/ads/AdRepository** - хранилище рекламных данных
- **model/geo/Locator** - геолокация
- **model/DataManager** - содержит методы для получения сложных данныx из разных источников
- **model/BasePresenter** - базовый presenter, принимает от SomeUi на вход query,
    выполняет его асинхронно в методе doQuery, оповещая SomeUi об изменениях своего состояния
- **model/SomePresenter** - наследует BasePresenter, содержит методы и поля,
    нужные конкретному Ui для отображения и изменения данных, обычно реализует метод doQuery
- **ui/MainActivity** - главное и единственное активити приложения
- **ui/common/base/BaseUi** - базовый класс для экрана
- **ui/main/MainUi** - логика частей интерфейса привязанных к MainActivity (bottom navigation, drawer и т.п.)
- **ui/SomeUi** - конкретный экран, наследует BaseUi, подписисывается на SomePresenter,
    переопределяет updateView(), в нем нужно обновить интерфейс в данными из SomePresenter
- **ui/SomeController** - контейнер с входными данными для SomeUi, также используется для сохранения/восстановления состояния SomeUi
    пришедшего в arguments инициализирует нужный Ui
- **ui/SomeBinding** - класс связывающий некие данные с их отображением, обычно подается на вход BaseRecyclerAdapter
- **ui/BaseRecyclerAdapter** - универсальный адаптер для RecyclerView, принимает список bindings,
    который определяет что этот адаптер может показывать
- **ui/common/StickyContainer** - универсальная показывалка стики хедеров/футеров поверх RecyclerView.
    Принимает на вход ViewGroup куда поместить стики-хедер (обычно это FrameLayout поверх RecyclerView)
    и Binding того что должно отображаться в стики-хедере.
    Также нужно переопределить метод getStickyItem и опционально getEdgeStickyItem.
    getStickyItem принимает на вход айтем из адаптра RecyclerView,
    если этот айтем должен быть стики, то метод должен вернуть подходящий айтем для Binding стики-хедера.
    getEdgeStickyItem должен вернуть айтем если нужно показать стики-хедер даже если список еще не проскроллен.
- **metrics/Metrics** - события аналитики, события отправляются в несколько Collector'ов аналитики.
    В какие аналитики отправлять события определяется ответом Api.getAnalytics
- **metrics/SomeKit** - враппер для стороннего SDK, может имплементить Collector
- **platform/WebAppSession** - обертка над инстансом WebView для его переиспользования на разных инстансах Ui
- **model/webapp/handler/...** - обработчики для методов бриджа, [поддерживаемых приложением](https://wiki.yandex-team.ru/edadeal/architecture/webview-native-interaction/#types-webview-app)

# [deprecated] API краткая схема

## /entities
```
{
    segments: [ { id, title, iconUrl, level, ordernum, ageRating, slug, active } ],
    compilations: [ { id, title, iconUrl, level, ordernum, ageRating, type, slug, active } ],
    retailerTypes: [ { id, name, ordernum, compilationsOrder, active } ],
    retailers: [ { id, typeId, title, iconUrl, logoUrl, primaryColor, secondaryColor, totalOffers, slug, shareUrl, label, isFavourite } ],
    radiuses: [ { factor, description } ]
}
```

## /location/info
```
{
    location: { id, name, region, center, inflections, slug, shareUrl, geoid, yandexPathArray},
    catalogs: [ { id, shopIds } ],
    retailers: [ { id, typeId, title, iconUrl, logoUrl, primaryColor, secondaryColor, totalOffers, slug, shareUrl, label, isFavourite } ]
    shops: [ { id, retailerId, locality, address, pos, iconUrl, totalOffers, localityId, openHours, catalogIds, location, shareUrl, occupancy, isFavourite } ],
    radius
}
```

## /catalogs/\<uuid\>
```
{
    id, retailerId, coverUrl, conditions, main, dateStart, dateEnd, totalOffers, offers: { without retailerId, catalogIds }, shareUrl, isAnyShop
}
```

## /shops/\<uuid\>
```
{
    id, retailerId, locality, address, pos, iconUrl, totalOffers, localityId, openHours, catalogIds, location, shareUrl, occupancy, isFavourite
}
```

## /map/tile
```
{
    shops: [ { id, retailerId, locality, address, pos, iconUrl, totalOffers, localityId, openHours, catalogIds, location, shareUrl, occupancy, isFavourite }],
    clusters: [ { pos, iconUrl, objectsCount, shops } ]
}
```

# [deprecated] Процесс загрузки данных приложения (MainPresenter.loadData)
* loadData загружает данные из кэша и/или сервера и сортирует загруженные магазины по дальности от пользователя.
* Процесс запускается методом MainPresenter.queryDataUpdate при заходе в активити или нажатии на кнопки загрузки данных.
* queryDataUpdate проверяет необходимость запуска loadData (насколько данные старые, насколько сменилась геопозиция и т.п.).
* режим работы loadData контролируется флагами isNeedLoadNewData (нужны данные от сервера) и isNeedLoadNewDataByUser (юзер нажал обновить).
* Сначала загружаем из репо selectedCity и locatedCity.
* Ждем геолокацию максимум 4 сек если требуется (см waitForLocation).
* Если locatedCity не определен, запрашиваем locatedCity у сервера.
* Полученные данные влияют на lat lng, которые будут подставлены в дальнейшие запросы.
* Загружаем аналитику и купоны в отдельном потоке (см. loadUnimportantData).
* Если нужны данные от сервера загружаем их синхронно (см loadNewData), при этом будет выполнена сортировка по дальности (см sortRetailerShops).
* Если в итоге (после загрузки или изначально, если её не было) в репо нет данных, то загружаем репо из кэша.
* Если данные в итоге взяли не от сервера, то сортируем их по дальности от пользователя (см sortRetailerShops).
* Процесс загрузки (неважно был ли запрос к сереверу) трекается событием метрики LoadDataAll.
* Процесс загрузки данных от сервера трекается событием метрики LoadDataNet.

# [deprecated] Процесс загрузки данных от сервера (DataManager.load)
* Возможны 3 результата загрузки (Result):
    - OK - все успешно загрузилось.
    - PROBLEM - что-то незагрузилось (магазин, ритейлер, каталог), можем показать данные на главном экране.
    - ERROR - не загрузилось что-то важное (location/info, entities), не можем показать данные на главном экране.
* Сначала паралельно грузятся entities и location/info, в случае ошибки одного из них result = ERROR.
* В случае успешной загрузки любого из 2х запросов его данные сохраняются в репо.
* Когда оба запроса успешно загружены мы можем показать данные на главном экране, все последующие неудачные запросы приводят к result = PROBLEM.
* Загружаем параллельно по одному магазины, добавленные в избранное, но отсутствующиe в location/info.shops (см getMissingShopIds).
* Загружаем параллельно по одному ритейлеры, добавленные в избранное, ритейлеры магазинов добавленных в избранное,
ритейлеры чьи товары добавлены в корзину, но отсутствующие в location/info.retailers (см getMissingRetailerIds).
* Загружаем параллельно по одному каталоги (с товарами), ид которых есть в полученных данных, вначале грузятся каталоги избранных магазинов (см getCatalogIdsToLoad).
* Когда загрузка закончена в случае result != ERROR данные каталогов, магазинов и ритеейлеров сохраняются в репо.

# Схема экранов
```
Home --------------------------------> Offers ---|
 |                                               |
 |---> Compilations -----------------> Offers ---|
 |                                               |
 |---> Deeplink.Shops ---------------> Offers ---|
 |                                               |
 '---> Deeplink.Offer ----> Shops ---> Offers ---|
                                                 |
Favorite ----------------------------> Offers ---|---+-------------------------> Shops?
   |                                             |   |
   '---> Shops+                                  |   |---> Compilations?
                                                 |   |
Map ---------------------------------> Offers ---|   '---> Offer --------------> Shops!
                                                 |           |
Cart ---> Offer ---> Shops ----------> Offers ---|           '---> Feedback ---> Shops?
            |
            '------> Feedback ---> Shops?

Cashback ---> ?
```
- Compilations - нажатие на компиляцию создает бэкстек
- Compilations? - нажатие на компиляцию сбрасывает стек до предыдущего экрана (с обновлением выбранного таба на нем)
- Offer - оффер с похожими товарами, в стеке может находиться несколько подряд
- Shops - нажатие на магазин переводит в каталог с созданием бэкстека
- Shops+ - на экране можно только пометить избранное
- Shops? - нажатие на магазин сбрасывает бэкстэк до предыдущего экрана (с заменой shopId)
- Shops! - нажатие на магазин сбрасывает бэкстэк до предыдущего экрана каталога

# Процесс запуска

Псевдо-код последовательности событий. Deeplink = deeplink, applink, shortcut
```kotlin
fun goDeeplink() {
    if (isNotCitySelected && isDeeplinkTargetNeedCity) {
        goCitiesIdentify()
    }
    goDeeplinkTargetUi()
}

fun start() {
    if (isDeeplink) {
        goDeeplink()
    } else {
        if (isNotTutorialShown) {
            goTutorial()
        } else if (isMajorVersionChange) {
            goWhatsNew()
            if (isWhatsNewGoDeeplink) {
                goDeeplink()
                return
            }
        }
        if (isNotCitySelected) {
            goCitiesIdentify()
        }
        goHome()
    }
}
```

# Авторизация, AB-эксперименты

[Docs](https://docs.edadev.ru/auth.html#device)

AuthPresenter выполняет запросы:
- регистрация устройства (UsrApi.device POST+PATCH)
- авторизация юзера (UsrApi.auth)
- получение информации о юзере (UsrApi.me)
- AB-эксперименты (UsrApi.abt)
- деавторизация юзера (UsrApi.logout)

## Регистрация устройства:
- Для регистрации устройства собирается набор идентификаторов (DeviceCredentials): yandex_deviceId, yandex_uuid, google_adid, push_token и т п.
- Многие из этих идентификаторов приходят асинхронно, некоторые требуют наличие интернета.
- Если юзер оффлайн, то вызов ручки будет отложен до появления сети
- Первая регистрация проводится с помощью POST-запроса device.
- Каждый раз когда один из идентификаторов меняется требуется обновить регистрацию PATCH-запросом device.
- Если PATCH-запрос вернет 401, то нужно повторить запрос уже с POST
- Запросы к device снабжены автоповтором в случае неудачи с увеличивающейся задержкой (tryMultipleTimesWithExponentialBackoff).
- device возвращает идентификаторы authorization и duid, которые потом подставляются в хедеры каждого запроса (см AuthInterceptor)

## AB-эксперименты
- Usr.abt завязан на athorization+duid, поэтому он запрашивается при их смене, а также с определенной периодичностью при заходе в приложение.
- Полученные AB эксперименты применяются при последующем переходе на экран

## Авторизация
- Юзер может авторизоваться через один из auth sdk: яндекс, vk и google
- Процесс авторизации начинается с вызова активити (startActivityForResult) нужного sdk
- Полученный в onActivityResult intent и resultCode отдаются в метод loadToken конкретного sdk, который вернет token
- Далее процесс отличается для яндекс sdk и остальных
- Для яндекс sdk полученный токен отдается в ручку auth
- Для остальных sdk формируется PostData(url, postData) (см getYandexPassportPostData),
- postData отправляются на url в webView в LoginUi, в ответ на что должен прийти токен, который далее отдается в ручку auth
- После выполнения ручки auth она отдает новый набор ид authorization, uid, duid, которые потом подставляются в хедеры каждого запроса
- После ручки auth вызывается ручка me с даннными о пользователе (ФИО, аватар)

## Деавторизация
- Деавторизация требует вызова ручки logout.
- Eсли юзер оффлайн, он будет деавторизован, но вызов ручки logout отложится до появления сети
- Ручка вернет новые ид authorization, duid
- Если ручка logout вернет 401, то должна быть вызвана ручка device POST

# Карта

[Slippy map tilenames](http://wiki.openstreetmap.org/wiki/Slippy_map_tilenames#Mathematics)

# Корзина

## Дубликаты в корзине (cartPresenter.removeDuplicates)
- добавить товар в корзину
- пометить этот товар купленным в корзине
- опять добавить этот же товар в корзину -> в корзине 2 одинаковых товара (1 куплен)
- снять "купленность" с купленного товара -> в корзине должен быть 1 товар в количестве 2 шт

# Лента товаров

Сортировка по умолчанию (см OffersPresenter.offerComparator):
- сортировка офферов происходит в зависимости от режима либо списка целиком, либо внутри групп, разделенных хедерами
- сначала идут офферы в магазинах более близких к юзеру
- если окажется что магазины разных ритейлеров находятся на одинаковом расстоянии от юзера (на разных этажах ТЦ), то сортируем их по названию ритейлера
- смотрим бренды оффера, сначала должны идти те офферы, чью бренды идут раньше в списке брендов пришедших в promo.json (pinup)
- смотрим сегменты офферов, офферы, у которых не указаны сегменты 2го или 3го уровней идут позже тех, у которых указаны
- если сегменты 2го уровня у офферов разные, то сначала идут офферы у сегментов 2го уровня которых ordernum ниже
- если сегменты 2го уровня одинаковые, то сравниваем по ordernum сегментов 3го уровня
- в остальных случаях сравниваем по priceNew

# Картинки
- Обложка каталога (главный экран): 144х192
- Лого ритейлера (главный экран): 112
- Лого ритейлера (экран выбора избранных): 72
- Иконка ритейлера (карточка магазина): 32
- Иконка ритейлера (карточка товара): 24
- Картинка товара (экран товара): 260
- Картинка товара (карточка товара): 88
- Картинка товара (корзина): 64
- Иконка сегмента 1 уровень: 24
- Иконка сегмента 2 уровень: 70

# Arc flow
## Структура
- trunk - ветка с изменениями в следующий релиз
- releases/experimental/mobile/edadeal/android/x.y.z - релизная ветка с изменениями готовыми к отправке в Google Play
- users/(user_name)/EDADEALANDROID-123 - ветки для тикетов из трекера
- users/(user_name)/updateReadme, users/(user_name)/fixCodeStyle - ветки без заведённых задач

## Порядок работы
- Когда начинается работа над задачей - oбновляем trunk, создаем от него ветку, задача переносится в In Progress
- В процессе работы, для сохранности кода, есть смысл пушить изменения на сервер еще до открытия PR
- Когда автор считает что задача закончена, он публикует свой PR и переносит задачу в Code Review
- Когда PR проверен - ветка сливается в trunk и удаляется, задача переносится в Ready For Test
- При начале работы над новым релизом - повышаем версию в trunk и создаем новую релизную ветку
- Если в релизной ветке нашлись проблемы: открываем PR к релизной ветке
- Если PR из релизной ветки захотели перенести в trunk: открываем новый PR в trunk и делаем в нем черри-пик из релизной ветки
- Если PR из trunk захотели сделать хотфиксом для релиза: открываем новый PR в релизную ветку и делаем в ней черри-пик из PR в trunk

## Текст сообщения коммитов
В названии коммита указываем номер тикета и название нашей очереди, чтобы коммит связался с задачей на трекере.

- `EDADEALANDROID-123 add scanner deeplinks`
- `EDADEALANDROID-123 fix sort order in favoriteUi`
- `EDADEALANDROID-123 refactor sort order in favoriteUi`
- `EDADEALANDROID-123 optimize dataManager.load`
- `EDADEALANDROID-123`
- `update retrofit, okhttp`

Если нужно подробное описание коммита, то его надо добавить после пустой строчки:
```
EDADEALANDROID-123 refactor metrics

Blabla bla blabla bla bla bla blabla bla
bla bla blablabla bla.
```

# Guidelines
## Principles
- KISS - чем меньше методы/классы и их количество и чем проще код в них, тем меньше шанс ошибки, проще понять
- YAGNI - простое решение сейчас и возможный рефакторинг потом лучше, чем сложное сейчас, но с заделом на потом возможно ненужную гибкость
- DRY, SPOT - меньше мест делающих одно и то же, меньше шанс изменить одно забыв про другое
- TDD - стараемся писать тесты, в идеале тестируемость должна приводить к более простому коду
- понятность важнее экономии циклов CPU
- используем SOLID гайдлайны при рефакторинге когда простое решение начинает не справляться
- в скоупе задачи поощряется мелкий Opportunistic Refactoring
- код должен быть самоописуем, комментарии - фоллбэк если не удалось описать кодом (issue url, workaround etc.)

## Files/Classes
- **colors.xml** разбит на 2 блока - palette и color types.
    Цвета из palette должны использоваться **только** в colors.xml, так как они могут перетасовываться.
- **strings.xml** должнен быть отсортирован в алфавитном порядке
- **Res** - дополнение к ресурсам в R
- **AppModule** - избегать использования isDebug флага где-либо вне Modulе,
    чтобы избежать багов проявляющихся в проде, но не в дебаге

# Code style
- [Android Kotlin Guides](https://developer.android.com/kotlin/style-guide)
- [Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html)
- Все PR прогоняются через detekt, поэтому полезно выполнять локально `./gradlew :detekt` перед публикацией PR

## Mosaic naming
- Параметры для Mosaic-блоков именуются по следующему правилу ```Mosaic<BlockType>Params```. Пример ```MosaicSegmentCarouselParams```, ```MosaicRetailerTypeShopsParams``` и т. д.

## XML id naming
```kotlin
viewSomething // View, FrameLayout, LinearLayout, RelativeLayout, CardView etc
imageSomething // ImageView
textSomething // TextView
editSomething // EditText
recyclerSomething // RecyclerView
scrollSomething // ScrollView
```

## XML attribute ordering
```xml
<TextView
    style="@style/MyCoolStyle"
    android:id="@+id/textTitle"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_something="bla"
    android:padding_something="bla"
    android:something="bla" />
```

## Interfaces implementations and subclasses naming
При именовании реализаций интерфейсов, добавляем префикс, указывающий на особенности реализации:
* `Repository` -> `RoomRepository`
* `Binding` -> `OfferBinding`
* `Map` -> `HashMap`

Если особенностей выделить не удается, добавляем суффикс `Impl`:
* `Database` -> `DatabaseImpl`

При именовании наследников базовых классов, заменяем префикс `Base`:
* `BaseUi` -> `HomeUi`
* `BasePresenter` -> `CartPresenter`

## Форматирование и порядок элементов в файле/классе
- не злоупотребяем пустыми строками, код легче понять когда он перед глазами, необходимость скроллить снижает восприятие
- пустые строки должны разделять код на осмысленные блоки, которые в будущем могут стать кандидатами на Refactor-ExtractFunction,
- не пытаться ужать максимум кода в минимум строк в ущерб читаемости
- связанные функции лучше держать рядом
- более важные функции лучше держать выше
- однострочники лучше группировать в блоки без разделения строк

```kotlin
class AwesomeClass {
    override val description = "A"
    override var title = "B"
    private val icon = "C"
    private var logo = "D"
    val name = "E"
    var url = "F"

    companion object {
        fun create(name: String) = ...
    }

    constructor(title: String) {
        this.title = title
    }

    fun sum(a: Int, b: Int) = a + b
    fun sub(a: Int, b: Int) = a - b
    private fun clearUrl() { url = "" }

    fun doMagic(stuff: Stuff) {
        val tag = stuff[KEY_TAG]
        ...
    }

    enum class AwesomeEnum { Red, Green, Blue }

    class AwesomeSubClass {
        ...
    }
}

private const val KEY_TAG = "tag"
private const val MAX_COUNT = 42
```

## Variable/property naming
```kotlin
// wrong
val r = getResult()
// ok
val result = getResult()
// wrong
val itemList = listOf(...)
val itemSet = setOf(...)
val itemMap = mapOf(...)
// ok
val items = listOf(...)
val items = setOf(...)
val items = mapOf(...)
// wrong
val itemClickAction: (Item) -> Unit
val itemClick: (Item) -> Unit
// ok
val onItemClick: (Item) -> Unit
// wrong
val onlineStateObservable = Observable.something(...)
// ok
val onlineStateChanges = Observable.something(...)
```

## Boolean variables and functions
Boolean переменные, функции и лямбды возвращающие Boolean должны иметь префикс is, has, can
```kotlin
val isItemAddedToCart = cartItem != null
val canInsertBannerAfterPosition: (Int) -> Boolean
fun hasShop(id: Int) = db.shops.contains(id)
```

## Single-line functions
Если не нужен `;` и функция влезает в лимит, то лучше в одну строку.
Возвращаемый тип не нужен если он очевиден из выражения/имени.
```kotlin
// wrong
fun sum(a: Int, b: Int): Int {
    return a + b
}
// wrong
fun search(query: String) { currentQuery = query; startSearch() }
// ok
fun sum(a: Int, b: Int) = a + b
fun hasFavorites() = items.any { it.isFavorite }
fun getEntity() = Entity().apply { name = "omg" }
fun getCatalogs(ids: Set<Int>) = ids.mapNotNull { repo.getCatalog(it) }
fun setErrorShown() { isErrorShown = true }
fun getSomeObscureItems(): Map<ByteString, List<Item>> = repo.getItems(...)
```

## Boolean !
Отрицания воспринимаются хуже
```kotlin
// wrong
if (!isUpdating) showList() else showProgress()
// ok
if (isUpdating) showProgress() else showList()
```

## Boolean operation order
Приоритет булевых операций нужно указывать явно - уменьшает шанс ошибки, подчеркивает задумку автора
```kotlin
// wrong
if (a && b || c) ...
// ok
if ((a && b) || c) ...
```

## lambda braces
Если функция имеет больше 1 лямбды в аргументах, вынос последней лямбды за скобки не всегда очевиден
```kotlin
// wrong
repeat(n, {
    ...
})
// ok
repeat(n) {
    ...
}
// ok
items.mapTo(mutableSet()) { it.id }
items.associateBy({ it.id }, { it.name })
// wrong
items.mapTo(mutableSet(), { it.id })
items.associateBy({ it.id }) { it.name }
```

## Pair, Triple destructing
first, second, third менее очевидно чем имена (даже однобуквенные)
```kotlin
// wrong
getSomeComplexData()
    .map { Triple(it.retailer, it.shop, it.catalog) }
    .filter { it.first.isFavorite && it.second != null && it.third.isNotEmpty() }
// ok
getSomeComplexData()
    .map { Triple(it.retailer, it.shop, it.catalog) }
    .filter { (retailer, shop, catalog) -> retailer.isFavorite && shop != null && catalog.isNotEmpty() }
// ok
getSomeComplexData()
    .map { Triple(it.retailer, it.shop, it.catalog) }
    .filter { (r, s, c) -> r.isFavorite && s != null && c.isNotEmpty() }
```

## if/when formatting
```kotlin
// ok
if (isReady) go()
if (isReady) go() else wait()
// ok
if (isReady) {
    go()
}
// wrong
if (isReady) { go() }
if (isReady) { go() } else { wait() }
if (isReady(getState(context))) router.go(childUi?.tag?.let { controller.toClass(it) })
// wrong
if (isReady)
    go()
// wrong
when { isReady -> go() }
// wrong
when {
    isSometing -> doSometing()
}
```

## if vs when
в некоторых случаях if может быть нагляднее when
```kotlin
// wrong
if (isReady) {
    go()
} else {
    wait()
}
// ok
when (isReady) {
    true -> go()
    else -> wait()
}
// wrong
when (isReady) {
    true -> {
        go()
        run()
    }
    else -> {
        sit()
        wait()
    }
}
// ok
if (isReady) {
    go()
    run()
} else {
    sit()
    wait()
}
```

## return statement
Ранний return стоит использовать если это уменьшает вложенность/количество кода.
В противном случае он не несет пользы, а также делает невозможным Refactor-ExtractFunction
```kotlin
// wrong
fun send(message: Message): Result {
    val result = Result.UnknownError
    if (message.isEmpty()) {
        result = Result.NotReady
    } else {
        val status = api.send(message)
        if (status in 200..299) {
            result = Result.Ok
        } else if (status in 400..499) {
            if (status == 401) toast("not authorized")
            result = Result.ClientError
        }
    }
    return result
}
// ok
fun send(message: Message): Result {
    if (message.isEmpty()) {
        return Result.NotReady
    }
    val status = message.send()
    if (status in 200..299) {
        return Result.Ok
    }
    if (status == 401) {
        toast("not authorized")
    }
    if (status in 400..499) {
        return Result.ClientError
    }
    return Result.ErrorUnknown
}
// ok
fun send(message: Message): Result {
    if (message.isEmpty()) return Result.NotReady
    val status = message.send()
    if (status in 200..299) return Result.Ok
    if (status == 401) toast("not authorized")
    if (status in 400..499) return Result.ClientError
    return Result.ErrorUnknown
}
// wrong
fun getText(message: Message): String? {
    if (!message.author.isValid()) {
        log.d { "error author " + message.author }
        return null
    }
    if (!message.title.isEmpty()) {
        log.d { "error title " + message.title }
        return null
    }
    if (!message.body.isEmpty()) {
        log.d { "error body " + message.title }
        return null
    }
    return "${message.author}\n${message.title}\n${message.body}"
}
// ok
fun getText(message: Message): String? {
    if (!message.author.isValid()) {
        log.d { "error author " + message.author }
    } else if (!message.title.isValid()) {
        log.d { "error title " + message.title }
    } else if (!message.body.isValid()) {
        log.d { "error body " + message.title }
    } else {
        return "${message.author}\n${message.title}\n${message.body}"
    }
    return null
}
```

# Тесты
## Инструменты
- [kotlin.test](https://kotlinlang.org/api/latest/kotlin.test/index.html)
- [hamcrest](http://hamcrest.org/JavaHamcrest/)
- [Mockito](http://site.mockito.org)
- [mockito-kotlin](https://github.com/nhaarman/mockito-kotlin)
- [unmock-plugin](https://github.com/bjoernQ/unmock-plugin)
- [Robolectric](http://robolectric.org)

## Именование
Предпочтительно именовать тест-кейсы по такому шаблону: `A should do B when C`, `A should do B`, `A should not do b`.
Названия вроде `testLoadSaveExperiments` вынуждают вчитываться в происходящее внутри тест-кейса, когда `loadExperimentsJson() should return content, that was saved by saveExperiments()` сразу указывает на ожидаемый результат от работы методов без необходимости изучать код.

## Параметризированные тесты
Для проверки одного и того же кейса с множеством разных параметров можно использовать параметризированный тест (см. `ReceiptToQrStringTest`).
Если для каждого набора параметров требуется дополнительное описание, его можно передавать строкой (см. `GetShopIdFromHeaderForOfferTest`).

Почему плохо проверять один кейс с разными параметрами с помощью последовательных ассертов? Первый провалившийся ассерт прервет выполнение всех последующих, в итоге получится неполная картина результатов выполнения теста, и после починки упавшего набора данных может упасть следующий. Если же тесты для всего набора выполняются параллельно, сразу видны все наборы данных, при которых тест падает.

# Metrics hell
- **SegmentName3** - конкретный сегмент товара, 2го и выше уровня
- **OffersScreenProductView** - просмотр товара на любом экране, см OffersScreenType
- **OffersScreenAddToCartClick** - добавление в корзину на любом экране, см OffersScreenType
- **OffersScreenAppear** - показ конкретного таба на экране списка товаров
- **FromScreen** - предыдущий экран, но есть исключения, см LoginScreen
- **CBOffersScreenProductView**, **CBMainScreenAppear** - перехыватываем эти события у WebView в CashbackUi и добавляем к ним FromScreen="" в общем случае, или FromScreen=MainScreenCBWidget при переходе из карусели кэшбэков с HomeUi
- **CBOffersScreenProductView** - отправляем за просмотры карточек кэшбэка в карусели на HomeUi. Особые значения пропертей: CBOffersScreenType=MainScreenCBWidget, WebViewVersion=""

# Links
- [GitLab](https://git.edadev.ru/mobile/android)
- [Fabric](https://fabric.io/edadeal/android/apps/com.edadeal.android/dashboard)
- [Material Design Icons](https://github.com/google/material-design-icons)
- [Metrics events](https://docs.google.com/spreadsheets/d/1go6RFUW-msFCUMFnGG8UaIBT22R2EJW0UwaCXLXMbDg/edit#gid=0)
- [Yandex App Metrica](https://appmetrica.yandex.ru/application/list)
- [Api Docs](https://docs.edadev.ru)
- [Deeplinks](http://edalinks.herokuapp.com/)
