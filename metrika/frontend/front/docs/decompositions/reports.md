# Перенос отчетов

## Общие замечания:

### В sagas/reportPage

parseUrl*() (переименовал в prepareReportData) вызывает yield* put(buildReportAction());
_parseUrl переименовал в parseUrl — надо выносить из саг и делать единый механизм работы с урлами в приложении.
В самом методе намешана логика парсинга serachParams и приведения их к параметрам отчета — тоже надо разделять на два метода.

В сагах много того, что нужны выносить в хелперы/мапперы, сделав саги "чистыми" (без yield) (metrika/client/store/reports/common/sagas/index.ts)

В сагах встречается последовательные вызовы большого числа экшенов через put. Это не очень хорошо с точки зрения перформанса, надо объединять или батчить.

## Проблемы

1. Много похожих отчетов, логика формирования которых отличается в деталях;
2. Реализовано несколько разных подходов (наследование, flow);
3. Не плоский стор, с дублированием данных в разных частях стора (касается не только отчетов);
4. Тяжело менять логику, запутанный код;
5. Используются недокументированные библиотеки (flow, ducks), что означает высокий порог входа для новых разработчиков и необходимость поддержки либ;
6. Проблемы с производительностью.

## Организация redux-store

![store](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-23T18%3A58%3A11.642091.png)

В корне стора сейчас содержится 8 ключей относящихся к отчетам (отмечено красным) и еще 4 связанных со стором (сегментация, выделено желтым).
Частично данные в разных ключах дублируются, плюс часть данных дублируется с частями, не относящимися к отчетам (например, report.counter дублирует данне из counter.activeCounter)

Подобный подход плох тем, что:
- Засоряется корень стора, тяжело считывать данные
- Приходиться реализовывать больше кода для обновления и считывания данных из разных мест
- Нет единой точки правды, дублирующиеся данные могут разъехаться между собой

Частично, необходимости большого количества ключей в сторе объясняется желанием сделать возможность асинхронного подключения редюсеров для каждой конкретной страницы (чтобы не делать инициализацию всех ключе сразу).
Подобный подход был бы оправдан, в случае, если бы инициализация и последующее хранение нулевого состояния было бы затратным, на практике обычно нулевое состояние легковесное, реальной экономии нет.
В дальнейшим предлагаю отказаться от асинхронной инициализации стейта, так как это существенно усложняет код и не дает положительного эффекта по производительности.

### Для новых отчетов и страниц:
- Держим все данные контекстно вместе, по одному ключу
- Избегаем дублирования данных
- Отказываемся от асинхронной инициализации
- Отказываемся от ducks в пользу redux/toolkit

## Про Flow

Не очевидна необходимость реализации flow, так как подобное может реализоваться на "чистом" js.
В качестве примера:

```tsx
// реализация на flow
const buildReport = createFlow((methods, ducks) => {
    const params = methods.prepareData();

    const res = methods.fetch();

    yield* put(methods.updateReport(res));
});

// реализация на "чистом" js
buildReport(methods, params) {
    const params = methods.prepareData();

    const res = methods.fetch();

    yield* put(methods.updateReport(res));
}
```

В данный момент у нас используется 65 различных flow. При этом, используем более одого раза мы только 15 flow.

Список переиспользуемых flow:

restoreDimensionsFlow - 2
restoreAttributesFlow - 2
restoreSortFlow - 2
restoreMetricsFlow - 2
paramsWatcherFlow - 2
initSegmentationMetadataFlow - 2
localizeFlow 2 - (состоит из двух вызовов)
parseSegmentationFlow - 2
getCustomComparableValueFlow -3
initUrlSerializeFlow - 3 (та самая логика парсинга урла, которая должна быть общей для всего приложения, точно сага здесь не нужна)
initInitializeFlow -4 (но состоит из одного единственного вызова call, вообще нет смысла в таком flow)
commonRestoreFlow - 4
initNoRobotsSettingFlow - 4
getInitialValueFlow - 4
apiRequestFlow - 15

Самый популярный flow (apiRequestFlow, 15 вызовов) выглядит следующим образом:

```typescript
export const apiRequestFlow = <M extends ApiRequestMethods<any, any>, O, B>(
methods: M & ApiRequestMethods<O, B>,
) =>
createFlow(function* (ducks, methods: ApiRequestMethods<O, B>) {
const options = yield* call(methods.getOptions, ducks);

    const data = yield* call(methods.getData, ducks, options);

    return data;
})(methods as M);
```

То есть два максимально абстрактных вызова, совсем не ясно, зачем это делать переиспользуемым.
Часть flow легко заменить, если передавать параметры в action.

Остальные 40 flow вызываются лишь единожды, что означает, что их применение не оправданно.

## Задачи

### 1. Рефакторинг ReportPageTouch

Необходимо вынести в контейнеры селекторы и подготовку данных, плюс вынести в контейнер механику построения самого отчета (то что сейчас в useComponentDidMount)
В компоненте должна остаться только визуальная часть

### 2. Рефакторинг стора

Переходим от плоского хранения в сторе к хранению всего внутри report.
Убираем дублирование данных

1. Отказываемся от всего, что сейчас есть в reportPage. В reportPage переносим report, reportLegend, reportMetadata.
Отказываемся от reportType (уже есть в report).
2. savedReports, favoriteReports & popularReports объединяем под ключом reportMenu
3. Объединяем segments, savedSegments, segmentationMeta, segmentationTree под ключом segmentation
4. Устранить дублирование между reportMetadata и report.metadata
5. Устранить дублирование между report.segments и reportMetadata.segments

### 3. Перенос legacy-отчетов: Роботы

- Ручка /internal/metrage/stat/v1/data

Параметры запроса в api:

```javascript
{
    preset: 'robots_all',
    offset: number,
    limit: number,
    include_undefined: true
    include_annotations: false,
    group: 'day' | 'week', 'month',
    date1: '2021-09-18'
    date2: '2021-09-24',
    id: number;
}
```

### 4. Перенос legacy-отчетов: Результат проверки (зависит от 3)

Нужен дизайн для мобильной метрики

- Ручка /stat/v1/custom/monitoring/log

Параметры запроса в api:

```javascript
{
    offset: number,
    'per_page': number;
    date1: '2021-09-18';
    date2: '2021-09-24';
    id: number;
    sort: 'from';
}
```

### 5. Перенос publishers-отчетов: Сводка (зависит от 3)

По паблишер-отчетам нужен дизайн
### 6. Перенос publishers-отчетов: Материалы

### 7. Перенос publishers-отчетов: Рубрики

### 8. Перенос publishers-отчетов: Авторы

### 9. Перенос publishers-отчетов: Тематики


