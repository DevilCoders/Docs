#Элемен "Истории успеха"

Позволяет получить доступ к локализованному массиву историй успеха.
Используется только при серверной шаблонизации.
При сбоке используется файл `desktop.blocks/i-utils/__success-stories/all.stories.json`.
Его необходимо перегенерировать при обновлении историй успеха в бункере и вкоммитить в репозиторий.
Файл `desktop.blocks/i-utils/__success-stories/all.stories.json` генерируется скриптом `data3/utils/success-stories/success-stories.js`
В make файле есть target `.PHONY: success-story` который запускает скрипт `data3/utils/success-stories/success-stories.js`
