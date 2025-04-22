# Настройка селективности для проектов

> ⚠️ Документация по инструменту [selectivity](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/selectivity/README.md)

## Настройка конфига

- Убедиться, что проект покрывается масками из корневого [конфига](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.config/selectivity.conf.js) селективности (смотреть в значение свойства `projects`), в противном случае описать маску по аналогии с другими проектами
- Добавить конфиг селективности относительно корня проекта по пути `.config/selectivity.conf.js` (поддерживаются также `json` и `yaml`-форматы)
- Настроить селективные проверки для своего проекта (в качестве примера можно использовать конфиг селективности из [ydo](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/ydo/.config/selectivity.conf.js))
- Список всех селективных проверк указан в корневом [конфиге](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.config/selectivity.conf.js) (смотреть в значение свойства `projects['*'].checks`)

## Селективность по платформам

На данный момент селективность по плафтормам настроена для проверок:
- `hermione`
- `e2e`
- `pulse:shooter` (селективность по платформам настроена хаком через разделение на проверки `pulse:shooter:desktop` и `pulse:shooter:touch` из-за [баги](https://st.yandex-team.ru/FEI-17631) в графовой оркестрации *Trendbox CI*)

При настройке селективности по платформам для какой-то из вышеперечисленных проверк необходимо убедиться, что каждая из платформ проекта описана в списке [доступных платформ](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/frontend-ci/src/command-helpers/format-jobs-data/constants.ts), в противном случае добавить новую платформу в список.

> ⚠️ Для корректной работы селективности по платформам для проверок `hermione` и `e2e` требуется версия инструмента `hermione>=3.10.1`

## Как добавить новую селективную проверку?

- Добавить проверку в список [доступных селективных проверок](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/frontend-ci/src/command-helpers/format-jobs-data/constants.ts)
- Добавить проверку в корневой [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.config/selectivity.conf.js) селективности по аналогии с другими проверками (смотреть в значение свойства `projects['*'].checks`)

## Как добавить селективность по плафтормам для произвольной проверки?

Настройка селективности по платформам для какой-то из проверок, скоее всего, потребует правок *ci*-скриптов, которые запускают эту проверку, поэтому рекомендуется [обратиться](https://forms.yandex-team.ru/surveys/17756/) в поддержку.
