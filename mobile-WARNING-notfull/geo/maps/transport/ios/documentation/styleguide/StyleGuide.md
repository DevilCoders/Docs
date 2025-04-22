# YandexTransport iOS StyleGuide

## Общие сведения

Данный документ обобщает стилистику написания кода iOS приложения Яндекс.Транспорт. Рассматривается только написание кода на **Swift**, в связи с очень незначительным количестовм кода на **Objective-C** в проекте.

За основу взят общий [Swift StyleGuide Яндекса](https://bb.yandex-team.ru/projects/MOBILECOMMITTEE/repos/swift-styleguide/browse), которому необходимо следовать во всех случаях, когда это не противоречит данному StyleGuide.

## SwiftLint

В качестве инструмента для обеспечения соответствия кода StyleGuide в проекте используется [SwiftLint](https://github.com/realm/SwiftLint). Правила конфигруруются так, что все warning'и трактуются, как ошибки.


## Правила

Используемые правила находятся в файле .swiftlint.yml в корне репозитория проекта. Ниже приведен список правил с параметрами, проверямых с помощью SwiftLint.


### [Line Length](https://github.com/realm/SwiftLint/blob/master/Rules.md#line-length)

Длина строк кода не должна превышать 120 символов.

#### Перенос строк

Для приведения кода в соответствие с данным правилом часто возникает необходимость делать переносы строк. Ниже приведены некоторые примеры того, как это следует делать в определенных ситуациях. 

##### Аргументы функций

Если функция в месте своего определения или вызова не может быть записана со всеми своим аргументами в строку длиной менее 120 символов, то следует ставить перенос строки после первого аргумента и всех последующих.

Например, функцию:

```swift
func someFunction(withArguments argumentA: TypeA, argumentB: TypeB, argumentC: TypeC, argumentD: TypeD) -> TypeE

```

Можно записать в виде:

```swift
func someFunction(withArguments argumentA: TypeA, 
                  argumentB: TypeB, 
                  argumentC: TypeC, 
                  argumentD: TypeD) -> TypeE

```

В тех случаях, когда даже при таком переносе, какая-либо из строк не умещается в 120 символов (например, из-за слишком длинных имен типов аргументов) следует попробовать переименовать функцию/типы/имена аргументов.
Если это по каким-либо причинам сделать нельзя, то в редких случаях допускается перенос строки перед первым аргументом функции.

К примеру:

```swift
func someFunctionWithLongName(andArgument argument: TypeOfTheFirstArgumentThatIsNotPossibleToMakeShorterDefinitely)

```

Так:

```swift
func someFunctionWithLongName(
        andArgument argument: TypeOfTheFirstArgumentThatIsNotPossibleToMakeShorterDefinitely)

```

##### Возвращаемые значения функций

В случае, когда имя типа возвращаемого значения функции слишком длинное, допускается перенести его на отдельную строку.

Например: 

```swift
func someFunction(withArgument argument: ArgumentType) -> SomeTypeWithRidiculoslyEnormousNameUsedAsReturnTypeOfSomeFunction

```

Таким образом:

```swift
func someFunction(withArgument argument: ArgumentType) 
        -> SomeTypeWithRidiculoslyEnormousNameUsedAsReturnTypeOfSomeFunction

```


### [Comma Spacing](https://github.com/realm/SwiftLint/blob/master/Rules.md#comma-spacing)

Перед запятой не должно быть пробелов, после запятой должен быть ровно один пробел.


### [Colon](https://github.com/realm/SwiftLint/blob/master/Rules.md#colon)

Между идентификатором и двоеточием не должно быть пробелов в определениях типов и словарных литералах.


### [Control Statement](https://github.com/realm/SwiftLint/blob/master/Rules.md#control-statement)

Условия или аргументы в выражениях `if`, `for`, `guard`, `switch`, `while` и  `catch` не должны обрамляться в необязательные внешние скобки.


### [Compiler Protocol Init](https://github.com/realm/SwiftLint/blob/master/Rules.md#compiler-protocol-init)

Инициализаторы определенные в протоколах компилятора, например `ExpressibleByArrayLiteral` не должны вызываться напрямую.


### [Deployment Target](https://github.com/realm/SwiftLint/blob/master/Rules.md#deployment-target)

Проверки с помощью `@available()` и `#available()` не должны производится для версий, которые подразумеваются в значении Deployment Target.
