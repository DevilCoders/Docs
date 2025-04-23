## Заметки об общем DivView контейнере

### Контракты

#### Описание дивы

```kotlin
data class DivInfo(
    val cardInfo: DivCardInfo,
    val logId: String? = null
)
```

Собственно основные данные для отображения дивы

#### Описание карточки

```kotlin
class DivCardInfo(
    val card: JSONObject,
    val templates: JSONObject? = null
)
```

В карточке передается сама дива, которую вы хотите нарисовать. Вы так же можете передать шаблоны если хотите.

#### Конфигурация контенйера дивов

Чтобы система могла нормально создавать диву, ей нужны определенные зависимости. Этот класс способ их предоставить. Большая часть инфы описана в javadoc

```kotlin
class DivContainerConfiguration(...)
```

Также есть класс 

```kotlin
data class InitializationContext(...)
```

Через который поставляются важные зависимости для самого движка дивов

#### Процессор действий в дивах

Если вам нужен какой-то кастомный action внутри дивы, который вы каким-либо образом хотите специально обработать, вам необходимо реализовать этот интерфейс

```kotlin
interface DelegatingDivActionHandler {
    fun handleDelegatedAction(action: DivAction, view: DivViewFacade): Boolean
}
```

и передать его в конфигурацию. Старайтесь обрабатывать только ваши действия, чтобы система работала корректно.

#### Внешнее состояние приложения

Для переменных и action trigger'ов вы возможно захотите поставить какое-то внешнее состояние - это можно сделать с помощью кастомной имплементации класса

```kotlin
interface IntrinsicState {
    fun reset()
    val stateChangeEvents: Flow<Unit>
}
```

#### Дива

Ну и собственно сама рендер дивов - вьюха 

```kotlin
open class DivContainerView
```

Вы даже можете ее засабклассить если необходимо, но лучше пользоваться предоставленными хуками. Описание смотрите в javadoc, важно помнить что это андроидный ViewGroup и имеет методы setup/rebind/update.

### Как этим пользоваться

Для начала через ваш DI вы должны собрать ряд зависимостей, таковыми являются

1. Реализация DelegatingDivActionHandler, можно просто noop
1. Инстанс DivImageLoader
1. Инстанс Div2Logger если необходимо
1. Реализация ExtensionInitializer если необходимо инициализировать div extensions или noop если нет необходимости
1. Реализация DivCustomViewAdapter если вы хотите поставлять свои div custom view или noop если нет необходимости
1. Инстанс InitializationContext в которую вы передадите необходимые сущности для инициализации дивы
1. Реализацию интерфейса IntrinsicState в которой вы поставляете какие-то внутренние переменные из своего приложения, или noop если такая функциональность не требуется
1. Необходимые реализации для описанных хуков
1. Инстанс DivContainerConfiguration собранный из полученных на предыдущих пунктах сущностей

Далее вы обычным способом какой вам наиболее удобен создаете DivContainerView и вызываете метод setup с контентом для отображения и собранными зависимостями.

Вы также можете пользоваться методом isRebindable/rebind для обновления контента в DivContainerView без его пересоздания.

Если не хотите думать над тем, что вызывать setup или rebind - пользуйтесь update, она умеет принимать такое решение правильно автоматически.

### Где посмотреть реализацию

Например в центавре (ДСЭ)

1. Часть зависимостей объявляются тут https://a.yandex-team.ru/arc_vcs/smart_devices/android/centaur-app/src/main/java/ru/yandex/quasar/centaur_app/dagger/DivModule.kt
1. Вторая часть (DivContainerConfiguration) ввиду того, что требуется Activity Context объявляется тут https://a.yandex-team.ru/arc_vcs/smart_devices/android/centaur-app/src/main/java/ru/yandex/quasar/centaur_app/ui/di/Div2Module.kt
1. Непосредственное использование можно посмотреть например тут https://a.yandex-team.ru/arc_vcs/smart_devices/android/centaur-app/src/main/java/ru/yandex/quasar/centaur_app/scenarios/DivContentFragment.kt 