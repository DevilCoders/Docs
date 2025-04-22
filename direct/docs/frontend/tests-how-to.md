# Часто задаваемые вопросы

## Как запустить локально тесты с дампами { #run-with-dumps }

```
npm run deploy

OVERRIDE_HASHSUMS=1 npm run hermione:standalone -- --set frozen --play --grep <GREP>
```

Пример:

`OVERRIDE_HASHSUMS=1 npm run hermione:standalone -- --set frozen --play --grep "Объявления: редактирование ТГО Уточнения Добавление существующего уточнения и выключение уточнения"`

## Как переснять дампы { #new-dumps }

Ссылка на документацию [тут](how-to-refresh-dumps.md).

## Как обновить скриншот { #new-sreenshot }

Ссылка на документацию [тут](tests-reuse-report.md).

## Тест в ПР то проходит, то нет { #flaky-test }

Посмотреть тесты которые "плохо" себя вели за последние 6 дней можно [тут](https://charts.yandex-team.ru/preview/editor/sadjdao38tqwm)
