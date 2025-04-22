# Релизы canvas


## Сборка

Стандартная java-овая:

{% include [этот релиз собирается в Newci](_includes/java-newci.md) %}

1. Убедиться, что никто не тестирует аналогичный релиз(если релиз есть, то не получится занять тестинг)
2. Проверить, что в trunk'е нет упавших тестов на CI: <https://ci.yandex-team.ru/project/112>
3. Написать, что планируете собирать релиз в [direct-release группу](../../reference/chats.md#direct-release) "Собираю релиз канваса"
4. Пойти в интерфейс NEWCI и нажать кнопку `Run release`

## тестирование

Регрессия запускается вместе с релизами web-dna. В релизе канваса своей регрессии нет. Поэтому нужно
1. Дождатся когда тикеты в релизе будут проверены
1. Просмотреть все тикеты "разобраться"

{% include [testing-done-footer](_includes/java-testing-done-footer.md) %}

## Ссылки { #links }

- тестовое окружение в ЯДеплое: <https://deploy.yandex-team.ru/stages/direct-canvas-test>
- devtest окружение в ЯДеплое: <https://deploy.yandex-team.ru/stages/direct-canvas-devtest>
