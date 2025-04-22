# Использование Combine (OpenCombine backport)

* Статус: Принято
* Ответственные: [coreshock](https://staff.yandex-team.ru/coreshock)
* Дата: 2020-07-02

Тех.история: [Форма подачи объявления](https://st.yandex-team.ru/VSAPPS-6894)

## Контекст

Форма подачи объявления (ФП).<br/>

## Причины

* Интенсивная работа с UI (обратная связь от пользователя): ввод текста, тапы на кнопки, навигация по форме и тд.
* Большое количество связей между элементами интерфейса
* Запрос рынка и команды разработки на интеграцию Functional Reactive Programming (FRP)

## Рассматриваемые варианты

* [RxSwift](https://github.com/ReactiveX/RxSwift)
* [ReactiveSwift](https://github.com/ReactiveCocoa/ReactiveSwift)
* [Combine](https://developer.apple.com/documentation/combine)
* [OpenCombine](https://github.com/OpenCombine/OpenCombine)
* [CombineX](https://github.com/cx-org/CombineX)
* Собственное решение

### Критерии

* Ограничения: iOS 11, Swift 5
* Стандарт или Стандартное решение
* Open Source
  * Покрытие тестами
* CocoaPods-совместим
* Поддержка типизированных ошибок

## Принятое решение

Выбран вариант: "OpenCombine", потому что:
* Удовлетворяет требованиям
* Предоставляет стандартное API Combine
* Работает на минимальной версии ОС – iOS 11.0
* Open Source, CocoaPods-совместим, Покрыт тестами
* Разработчики не распыляются на поддержку расширений
* Топовая реализация
* Реализация легко читается
* Для интеграции с RxSwift есть адаптер [RxCombine](https://github.com/CombineCommunity/RxCombine)

В целом различий между OpenCombine и CombineX не так много. Можно заменить на CombineX в случае увеличения его доли или в случае возникновения серьезных проблем.

### Позитивные последствия

* Сокращение количества кода
* Догоняем технологический стек
* Удволетворение потребностей рынка
* Легкий переход на официальный Combine
* Легкий переход на другую реализацию (например, CombineX)

### Негативные последствия

* Высокий порог входа
* Ступенчатое освоение парадигмы:
  * освоение основ FRP
  * освоение выбранной библиотеки
  * применение выработанных практик и шаблонных решений
  * изменение подхода с императивного на формирование потоков данных и их связывание как источник-потребитель

## Плюсы и минусы вариантов

### RxSwift (5.1.1)

http://introtorx.com/<br/>
http://reactivex.io/<br/>
Звезд: 18637, Форков: 3358

Хороший, потому что:
* Стандартизирован (входит в [ReactiveX](http://reactivex.io/))
* Зрелый (версия 1.0 вышла 2 мая 2015)
* Имеет сложившееся комьюнити
* Имеет [хорошую документацию](https://github.com/ReactiveX/RxSwift/tree/5.1.1/Documentation)
* Покрыт тестами
* Имеет поддержку UI и тестов в стандартной поставке (RxCocoa, RxBlocking, RxTest)
* Имеет большое количество расширений, поддерживаемых комьюнити [RxSwiftCommunity](https://github.com/RxSwiftCommunity)
* Мажорные версии привязаны к версиям языка
* Open Source
* CocoaPods-совместим
* Удовлетворяет тех.требованиям: iOS 8.0+, Swift 5.0

Плохой, потому что:
* Нет поддержки типизированных ошибок ([Обсуждение](https://github.com/ReactiveX/RxSwift/issues/1320))

### ReactiveSwift (6.3.0)

https://reactivecocoa.io/<br/>
Звезд: 2633, Форков: 363

Хороший, потому что:
* Зрелый (версия 1.0.0 для Objective-C вышла 1 окт. 2016)
* Покрыт тестами
* Имеет поддержку UI ([ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa))
* Имеет небольшое количество расширений, поддерживаемых комьюнити [ReactiveCocoa](https://github.com/ReactiveCocoa)
* Open Source
* CocoaPods-совместим
* Удовлетворяет тех.требованиям: iOS 8.0+, Swift 5.0
* Есть поддержка типизированных ошибок

Плохой, потому что:
* Нестандартизирован

### Combine

https://developer.apple.com/documentation/combine

Хороший, потому что:
* Является пакетом экосистемы Apple
* [Эффективнее RxSwift](https://quickbirdstudios.com/blog/combine-vs-rxswift/)
* Имеет небольшое количество расширений, поддерживаемых комьюнити [CombineCommunity](https://github.com/CombineCommunity)
* Есть поддержка типизированных ошибок
* API похоже на стандарт [Reactive Streams](https://www.reactive-streams.org/)

Плохой, потому что:
* Proprietary
* Не удовлетворяет тех.требованиям: iOS 13.0+
* Поддержка UIKit сторонними решениями ([CombineCocoa](https://github.com/CombineCommunity/CombineCocoa))

### OpenCombine (0.9.0)

https://github.com/OpenCombine/OpenCombine<br/>
Звезд: 1249, Форков: 81

Хороший, потому что:
* Combine API-совместим (почти полностью)
* Open Source
* CocoaPods-совместим
* Удовлетворяет тех.требованиям: iOS 8.0+, Swift 5.0
* Поддерживается 13 разработчиками

Плохой, потому что:
* Нет поддержки UIKit, но можно легко портировать, заменив импорты ([CombineCocoa](https://github.com/CombineCommunity/CombineCocoa))
* Практически нет комьюнити и расширений, но, по необходимости, можно портировать расширения из [CombineCocoa](https://github.com/CombineCommunity/CombineCocoa)

### CombineX (0.2.1)

https://github.com/cx-org/CombineX<br/>
Звезд: 411, Форков: 23

Хороший, потому что:
* Combine API-совместим (почти полностью)
* Имеет поддержку UI ([CXCocoa](https://github.com/cx-org/CXCocoa))
* Имеет небольшое количество расширений, поддерживаемых комьюнити [CombineX](https://github.com/cx-org)
* Open Source
* CocoaPods-совместим
* Удовлетворяет тех.требованиям: iOS 8.0+, Swift 5.0

Плохой, потому что:
* Код многословный, тяжело читается
* Поддерживается 3 разработчиками

### Собственное решение

Хороший, потому что:
* Можно выбрать любой стандарт
* Можно взять код из любых проектов за основу
* Можно задать любые ограничения на совместимость

Плохой, потому что:
* Огромные трудозатраты (предварительно от 2 месяцев)
* Ограниченность ресурсов поддержки
* Proprietary

## Ссылки

* Связано с [ADR-0002](0002-collectionviewmodel-binding.md)
