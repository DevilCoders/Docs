

Контейнер помогающий писать эксперименты в декларативном стиле

Для использования нужно обеспечить наличие коллекции **experimentFlag** в стейте
(К примеру через резолвер **resolveExperimentFlagsSync**)

**Example**
```jsx static
<div>
    <RenderIfExperimentEnabled experimentFlagId="all_some_experiment_id">
        Рендерится если пользователь попал в эксперимент all_some_experiment_id
    </RenderIfExperimentEnabled>

    <RenderIfExperimentEnabled experimentFlagId="all_some_experiment_id" experimentFlagValue="some_experiment_value" >
        Рендерится если пользователь попал в эксперимент all_some_experiment_id со значение сплита = some_experiment_value 
    </RenderIfExperimentEnabled>
</div>
```
