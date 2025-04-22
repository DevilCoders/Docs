# lcActions

`lcActions` - синглтон в [Конструкторе лендингов](https://lpc.yandex-team.ru), используемый в Lc-секциях для хранения и работы с действиями. Действие - метод секции через который можно изменить её состояние, он может быть вызван по событию или откуда то ещё.

Все действия определяются в компоненте секции и привязываются к синглтону через метод `setSectionData`, так же в этом методе зашита логика вызова действий в редакторе через `postMessageChannel` (используется для активации модального окна через кнопку или открытия таба при клике по вложенной секции в дереве).

## Примеры

### setSectionData
`lcActions.setSectionData(sectionId, LcSectionType.LcTabs, { [LcEventAction.ChangeTab]: this.onChangeTab });`

`sectionId` - строка с идентификатором секции пришедшим из конструктора, если идентификатор не пришёл берём якорь

`LcSectionType.LcTabs` - тип секции

`actions` - объект с действиями секции

### removeSectionData
`lcActions.removeSectionData(sectionId);`

### showSectionByAnchor
`lcActions.showSectionByAnchor(anchor);`
