[![Build status][2]][1]

  [1]: https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Disk_Web_Helpers_TestPr&branch_Disk_Web_Helpers=%3Cdefault%3E&tab=buildTypeStatusDiv
  [2]: https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Disk_Web_Helpers_TestPr)/statusIcon.svg (Go To Build Page)


## Общие хелперы Яндекс.Диска и смежных проектов

При добавлении нового функционала или модификации существующего API не забываем описать новый API
в формате [jsDoc](http://usejsdoc.org), собрать MarkDown-документацию
```
npm i
node generate-md.js
```
После выполнения последней команды убедиться, что документация собралась (в консоли должно быть `Done!`)

#### Описание хелперов

[lib/datasync](./md/datasync.md)

[lib/dialog](./md/dialog.md)

[lib/format](./md/format.md)

[lib/is-browser-supported](./md/is-browser-supported.md)

[lib/path](./md/path.md)

[lib/sortedIndex](./md/sortedIndex.md)

[lib/space](./md/space.md)

[lib/date/date-to-string](./md/date/date-to-string.md)

[lib/date/date](./md/date/date.md)

[lib/date/seconds-to-time](./md/date/seconds-to-time.md)

[lib/date/string-to-date](./md/date/string-to-date.md)

