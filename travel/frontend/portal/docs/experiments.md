# Эксперименты и Feature Toggle

## Uaas experiments

`uaasExperiments` - (usersplit as a service) эксперименты, которые приходят из сервиса [ab.yandex-team.ru](https://ab.yandex-team.ru)

### Пример конфигурации

```js
    uaasExperiments: {
        aviaTestExperiment: 'AVIA_experiment:test'
    },
```

|                    | Описание                        |
| ------------------ | :------------------------------ |
| AVIA_experiment    | ключ эксперимента               |
| test               | значение эксперимента           |
| aviaTestExperiment | название эксперимента в конфиге |

### Пример использования

```js
import experimentsSelector from 'selectors/common/experimentsSelector';

const mapStateToProps = state => ({
    experiments: experimentsSelector(state),
});
```

Для экспов в конфиге можно указать и boolean флаг, тогда применится значение этого флага, а внешнее управления(uaas/cookie) будет невозможно:

```js
    uaasExperiments: {
        aviaTestExperiment: true
    },
```

### "Небулевые" значения

Если у одного ключа может быть несколько значений в AB, то в конфиге
задаем "записи" под каждую пару `key1:value1, key1: value2, key1: value3 ...`, которые попадут затем в `reduxStore.common.experiments` в виде булевых флагов.

Пример:

```js
uaasExperiments: {
    aviaEnableSearchPage: 'AVIA_LOGIC_search:tech_release',
    aviaEnableOnlyPortalSearch: 'AVIA_LOGIC_search:only_portal'
}
```

В `reduxStore.common.experiments` тогда получим:

```js
experiments: {
    aviaEnableSearchPage: true,
}
```

либо

```js
experiments: {
    aviaEnableOnlyPortalSearch: true;
}
```

либо `experiments: {}`.

### Залипание в эксперименте

Залипание в эксперименте — принудительное попадание в эксперимент для целей разработки или тестирования.

Если эксперимент добавлен в сервис AB, то можно залипнуть через жука, вкладка "Эксперименты",
нужный эксперимент можно найти по названию или номеру эксперимента.

Для экспериментов, которые еще не добавлены в AB у нас есть свой механизм залипания через куки.

Например, для эксперимента из конфига `{ aviaTestExperiment: 'AVIA_experiment:test' }`
нужно поставить куку `AVIA_experiment=test` (`document.cookie = "AVIA_experiment=test; path=/;"`).
При этом в конфиге не должен стоять принудительный флаг: `{ aviaTestExperiment: true }`.

Для удобства в сервисе есть специальный UI `/test/experiments` для залипания в экспериментах.

## Feature Toggle

Фиче-флаги мы используются для наших внутренних нужд.

Например, мы можем их использовать, когда хотим временно скрыть какую-то функциональность от пользователя.

Настраиваются фиче-флаги в конфиге в поле `experiments`.

В текущей реализации `dataui/core` не предусмотрена возможность глубокого мёржа конфига.
Поэтому информацию о каждом эксперименте необходимо добавлять в каждый конфиг окружения.

#### Важно: нельзя просто так взять и изменить процент распределения у эксперимента!

Потому как новое распределение значений кук будет работать только для новых пользователей.
Так что, если нужно изменить процент распределения, необходимо завести новый эксперимент (с новым названием).
Разумеется речь идет только про прод и при разработке позволяется менять проценты эксперимента сколько угодно раз, но не увлекайтесь, потому что от этого, говорят, волосы на ладошках растут.

### Пример конфигурации фиче-флагов

```js
experiments: {
    booleanExperiment: {
       type: Boolean,
       percentage: 10 // для 10% пользователей значение booleanExperiment будет выставлено в true,
                      // у остальных – defaultValue
       defaultValue: true, // по умолчанию false для Boolean
       denied: true // означает, что будет использовано значение defaultValue и кука
                    // не будет выставляться пользователям. По умолчанию имеет значение false
   },

   numberExperiment: {
       type: Number,
       values: [
           {
               value: 20,
               percentage: 15 // для 15% пользователей значение numberExperiment будет выставлено в 20
           },
           {
               value: 100,
               percentage: 15 // для других 15% значение numberExperiment будет выставлено в 100
           }
       ],
       defaultValue: 10 // для остальных 70% выставляем 10
   },

   stringExperiment: {
       ...
       dependencies: { // зависимый эксперимент выставляется только тем пользователям,
                       // которые попали в родительские эксперименты, у остальных будет undefined

           booleanExperiment: [true],  // stringExperiment будет выставляться только тем,
                                       // у кого booleanExperiment равен true
           numberExperiment: [10, 20]  // и при этом numberExperiment равен 10 или 20
       }
       dynamic: true // Значение зависит от внешнего мира, при запросах его надо обновлять
                     // т.е. кука будет высчитываться и перезаписываться у пользователя
                     // при каждом запросе
   }

   funcExperiment: function (req) { // эксперимент в виде функции, возвращающей промис
       return new Promise((resolve) => {
         setTimeout(() => resolve({
             type: Boolean,
             percentage: 10
          }), 10);
       });
   }
}
```
