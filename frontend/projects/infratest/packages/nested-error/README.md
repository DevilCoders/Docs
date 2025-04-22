= Nested error

Класс ошибки с причиной. Позволяет выстраивать цепочки ошибок.

== Использование

== Deprecation notice

В стандарт ECMAScript добавлена опция cause у ошибок. Нужно либо закопать этот пакет либо сделать его полифиллом к стандарту.

Proposal: https://github.com/tc39/proposal-error-cause
Описание в стандарте: https://tc39.es/ecma262/multipage/fundamental-objects.html#sec-error-constructor
Поддерживается в v8, начиная с версии 9.3: https://v8.dev/features/error-cause
Поддерживается в nodejs начиная с 16.10: https://node.green/#ES2022-features-Error-cause-property