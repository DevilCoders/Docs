# @yandex-market/ya-vault-utils
Библиотека для работы с секретницей

## Установка
```bash
npm install @yandex-market/ya-vault-utils
```

## Использование

Обязательно должна быть установлена утилита ya

```typescript
import { getSecretValues, getSecretValueByKey } from '@yandex-market/ya-vault-utils';

const secretId = 'sec-01ehyck1p9vc10v3sdprcr93mm';
// возьмется последняя версия этого секрета и вернется словарик с его значениями
const secretValueBySecretId = getSecretValues({id: secretId});

const versionId = 'ver-01f1s4pr8bjbyn216gjq9ffj4g';
// возьмется указанная версия секрета и вернется словарик с ее значениями, не оч удобно если меняется 
const secretValueByVersionId = getSecretValues({id: versionId});

const valueKey = 't2m-monitor.postgresql.password';
// вернется строковое значение определенного значения в версии секрета
const secretValueByKey = getSecretValueByKey(secretId, valueKey);
```

## Сборка

```bash
npm run build
```

## Запуск тестов

```bash
npm run test
```
