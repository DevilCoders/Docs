# Codeshifts для компонентов

Для упрощения перехода на новые версии мы пишем миграционные скрипты.
Они позволяют автоматически трансформировать ваши исходники под изменения библиотеки (менять импорты, не подключать ненужные файлы и т. д.) без запуска `tsc` и ручной работы.

```bash
npm i -g jscodeshift
```
Подробнее про codeshift в репозитории проекта: https://github.com/facebook/jscodeshift

## Использование
```bash
jscodeshift --parser=tsx -t <pathToCodeshift> <Path/To/Src/For/Transform>
```
С релизом `@yandex-lego/components` поставляется папка `codeshifts`, где написаны миграции под разные версии.

## Написать свой codeshift
### Хелперы
У нас уже есть ряд хелперов, которые позволяют делать разные рутинные действия. Можете собрать нужную миграцию из наших утилитит:

- **removeImport.js** — удаляем определенные импорты;
- **removeProps.js** — удаляем props из jsx;
- **removeTypeReference.js** — удаляем определенный TypeReference;
- **removeUsage.js** — удаляем использование того, что вырезали из импортов;
- **filterCompose.js** — фильтруем композы;
- **isNotEmptyUnion.js** — проверка, что Union не пустой;
- **filterIdentifier.js** — убираем ненужные идентификаторы;
- **filterTypes.js** — убираем ненужные типы;
- **isEmpyCompose.js** — проверка того, что остался пустой compose/composeU;
- **isSpecificIdentifier.js** — проверка, является ли переданный Identifier тем, что нам нужно (valueIdentifier), можем проверить, например, что это `viewViewClassic`.

### Как писать codeshift
Необходимо создать модуль, который будет принимать информацию о файле и разные параметры от jscodeshifts.

```
module.exports = (fileInfo, { jscodeshift: j }) => {
    const root = j(fileInfo.source);
    // Производим различные операции над исходниками
    // Фильтруем импорты, удаляем использования и т. д.
    // Возвращаем обработанный код
    return root
        .toSource();
};
```

#### AST Explorer
https://astexplorer.net/

Это незаменимый помощник для написания кодшифтов.
Надо написать тот код, который вы хотите обрабатывать.
Изучить tree и написать правильные фильтры или заменители.

Как правило, все сводится к поиску нужного узла AST и его обработки.
Через `jscodeshift.find(..)` можно искать разные конструкции — от базовых до конструкций из TS и JSX (они, как правило, имеют в начале названия TS или JSX, например `TSUnionType` или`JSXOpeningElement`)

