
Контейнер помогающий писать эксперименты в декларативном стиле, отдаёт статус
эксперимента через render props, для случаев где нужен более гибкий API.

Для использования нужно обеспечить наличие коллекции **experimentFlag** в стейте
(К примеру через резолвер **resolveExperimentFlagsSync**)

**Example**

```jsx static
<div>
    <ExperimentStatus experimentFlagId="all_some_experiment_id">
        {({isEnabled}) =>
            isEnabled
                ? 'Пользователь попал в эксперимент all_some_experiment_id'
                : 'Пользователь НЕ попал в эксперимент all_some_experiment_id'
        }
    </ExperimentStatus>

    <ExperimentStatus experimentFlagId="all_some_experiment_id" experimentFlagValue="some_experiment_value" >
        {({isEnabled}) =>
            isEnabled
                ? 'Пользователь попал в эксперимент all_some_experiment_id'
                : 'Пользователь НЕ попал в эксперимент all_some_experiment_id'
        }
    </ExperimentStatus>
</div>
```
