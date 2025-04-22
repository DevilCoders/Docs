# Автоматическая генерация типов

## Подготовка

Предварительно необходимо установить arc и смонтировать его рабочую копию на свой компьютер –
https://docs.yandex-team.ru/devtools/intro/quick-start-guide.

## Использование

Для автоматической генерации типов на основе yaml-файлов используется утилита
taxi-typings (https://github.yandex-team.ru/ktnglazachev/taxi-typings).

Конфиг, необходимый для настройки утилиты – `/types.config.json`

Для добавления нового сервиса / репозитория с сервисами необходимо в данном конфиге добавить
сервис в объект targets / репозиторий в массив repositories по аналогии с уже подключёнными сервисами.

Генерация осуществляется в папку `/src/types/api/<repo_name>/<service_name>` командой `npm run typings`.
Если сервис всего один, то подпапка `<service_name>` не будет создана.

Если нужно сгенерировать типы какого-то определённого сервиса, следует добавить к команде параметр `--scope`, например:
```shell
# npm run typings -- --scope <repo>:<service>
npm run typings -- --scope backend-py3:atlas-backend
```

Если сервис перестал использоваться, нужно убрать его из конфига, а также вручную удалить сгенерированные типы.

## Применение сгенерированных типов

Не стоит использовать типы, экспортируя их непосредственно из места генерации.
Следует создать в используемом api файл `types.ts` через него экспортируя необходимые типы,
при необходимости уточняя типизацию (это может быть нужно, потому что генерация типов иногда выдаёт слишком общие типы):

Например:
```typescript
// Файл /src/types/api/repo/service/definitions.ts
export type ApiType1 = {
  value: number;
  status: string;
};
export type ApiType2 = number[];
```
```typescript
// Файл /src/api/service/types.ts
import {ApiType1} from 'types/api/repo/service/definitions';

export type {ApiType2} from 'types/api/repo/service/definitions'; // Реэкспорт полностью подходящего типа

// Модификация и экспорт неполного типа
export type Status = 'active' | 'inactive';
export type CorrectedApiType1 = Omit<ApiType1, 'status'> & {
  status: Status;
  isLoading: boolean;
}
```
