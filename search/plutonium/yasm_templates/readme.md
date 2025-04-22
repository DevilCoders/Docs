Описание и помощь с синтаксисом: https://wiki.yandex-team.ru/golovan/userdocs/templatium/alerts/

###  Как обновить шаблоны панелей и/или алертов?

1. Закоммитить изменения в шаблон
2. [опционально] запустить скрипт [run_templater.sh](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/yasm_templates/run_templater.sh) (из директории yasm_templates)
3. Перейти в [CI](https://a.yandex-team.ru/projects/saas2/ci/releases/timeline?dir=search%2Fplutonium&id=yasm-templates-release), прожать релиз, открыть флоу и запустить там таск Build YASM templates

П. 3 можно выполнить из пулл-реквеста еще до коммита (флоу "search/plutonium: Deploy YASM templates" в списке прекоммитных проверок)

### Как добавить новый шаблон?
1. Добавить шаблон в соответствующий список в скрипте [run_templater.sh](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/yasm_templates/run_templater.sh) (из директории yasm_templates)
2. Добавить шаблон в меню [saas2.json](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/yasm_templates/saas2.json)
3. Перейти к п.1 инструкции по обновлению шаблона

### Как найти шаблоны панелей?
Через [меню в Головане](https://yasm.yandex-team.ru/menu/saas2/)
