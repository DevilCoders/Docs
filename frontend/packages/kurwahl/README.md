# kurwahl

Инструмент для построения и работы с графом зависимостей с немецким ~~качеством~~ именем.

## Установка

```sh
npm i @yandex-ci/kurwahl --registry http://npm.yandex-team.ru
```

## Использование

…

## Описание

### Этимология

От Нем. уст. Kur «выбор» и Wahl «выбор».

### Характеристики

- Хранение зависимостей между:
  - пакетами по `lerna.json` + `package.json`/`package-lock.json` — маппинг файлов на версии пакетов (как в lerna);
  - узлами внутри пакетов (tbd);
  - узлами пакета и внешними, по отношению к пакету, модулями и ресурсами (tbd);
  - тестами и кодом в рамках пакета (tbd).
- Хранить соотношение пакетов с версиями и узлами внутри (абсолютные пути в относительные и назад, tbd).
- Прогрессивное-ленивое достроение графа (по требованию) — запоминаем как можно посчитать подграф, считаем при необходимости или когда можем (tbd).
- Считать какие тесты и кейсы затронуты по измененным файлам и мб экспортируемым сущностям внутри (tbd).
- Считать какие пакеты затроны изменениями — явно или косвенно (насколько близко к используемому месту, tbd).

Узлами внутри пакетов могут считаться:
- код модулей, а именно:
  - js/es-модули целиком;
  - экспортируемые значения и импорты модулей;
  - css-файлы (с его импортами);
- код продуктовых единиц (колдунщики, страницы, entrypoint-ы, и т.д.);
- тесты и конкретные тест-кейсы;
- другие файлы/ресурсы в качестве импортируемых в код и тесты ресурсов (шрифты, дампы, другое).

### Incomplete Dependency Graph (IDG)

```ts
interface IDGNode {
  type: string;
  meta: Meta;
}

interface IDGImport extends IDGNode {
  type: 'Import';
  schema: 'es';
  packageId: IDGPackageId | null;
  modulePath: string;
  for: string[] | null;
}

type SemverString = string; // "v1.0.0"-like strings
type IDGPackageVersion = SemverString | '*';
type IDGPackageId = string;
enum IDGRegistryType {
  npm
}

interface IDGRegistry {
  type: IDGRegistryType;
  url: URL;
}

interface IDGPackage extends IDGNode {
  id: IDGPackageId;
  registry: IDGRegistry;
  name: string;
  version: IDGPackageVersion;
  dependencies: IDGPackage;
  modules: IDGModule[];
}

interface IDGModule extends IDGNode {
  packageId: IDGPackageId;
  path: string;
  imports: IDGImport[];
  exports: Record<string, IDGExport>;
}

interface IDGExport extends IDGNode {
  value: ASTNode | IDGImportReference;
}

interface IDGCheck extends IDGNode {
  value: ASTNode | IDGImportReference;
}
```
