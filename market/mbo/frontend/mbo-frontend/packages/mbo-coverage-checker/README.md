# @yandex-market/mbo-coverage-checker
Библиотека для работы с тестовым покрытием
## Установка
```bash
npm install @yandex-market/mbo-coverage-checker
```

## Использование
Есть 3 ассинхроных метода 

writeCurrentCoverage - записывает покрытие (спасибо кеп)
compareCurrentCoverage - сравнивает покрытие (спасибо кеп)
принимают они одинаковые параметры 

dbOptions - конфиги для подключения к базе данных (используется постгресс)
projectOptions - конфиги проекта

startCoverageChecker - берет на себя все проверки, и в зависимости от переданного флажка записсывает или сравнивает покрытие

```typescript
import { startCoverageChecker } from '@yandex-market/mbo-coverage-checker';

const projectOptions = {
  projectName: 'ir-ui',
  envBranchName: 'master',
  reportPath: './coverage-summary.json';
};

const connectionOptions = {
  password: '123'
}

const IS_CHECK_COVERAGE = true;
const IS_DEPLOY = true;

if(IS_CHECK_COVERAGE){
  startCoverageChecker(IS_DEPLOY, connectionOptions, projectOptions);
}
```
ну или можно сделать свою проверку если оч хочется :))

```typescript
import { writeCurrentCoverage, compareCurrentCoverage } from '@yandex-market/mbo-coverage-checker';

const projectOptions = {
  projectName: 'ir-ui',
  envBranchName: 'master',
  reportPath: './coverage-summary.json';
};

const connectionOptions = {
  password: '123'
}

const IS_CHECK_COVERAGE = true;
const IS_DEPLOY = true;


const startChecker = async () => {
  if(IS_CHECK_COVERAGE){
    try {
      const result = await (isWrite ? writeCurrentCoverage : compareCurrentCoverage)(connectionOptions, projectOptions);
      // метод writeCurrentCoverage ничего не возвращает при усппешном выполнении
      // а вот compareCurrentCoverage в случае снижения покрытия возвращает массив с инфой по каждому типу покрытия
      // поэтому 
      if(result){
        exit(1);
      } else {
        exit();
      }
    } catch(error){
      console.log(error);
      exit(1);
    }
  }
}

startChecker();

```

## Сборка

```bash
npm run build
```

## Запуск тестов

```bash
npm run test
```
