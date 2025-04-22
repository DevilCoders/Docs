# Кодстайл Unit-тестов

1. Тесты пишем на английском.
2. `*.spec.ts` не пишем.

## Тесты на модули
1. Располагаются в `./__tests__/<name>.test.ts`.
2. `describe('#methodName', () => { it('returns ... when foo=bar') })`.

## Тесты на классы
1. Располагаются в `./__tests__/<name>.test.ts`.
2. `describe('ClassName', () => { describe('#method', () => { it('returns ... when foo=bar') }) })`.

## Тесты на компоненты
1. Располагаются в `./__tests__/<name>.test.ts`.
2. `describe('ComponentName', () => { it('... when foo=bar') })`.
