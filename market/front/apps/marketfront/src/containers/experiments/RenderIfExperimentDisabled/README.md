

Контейнер помогающий писать эксперименты в декларативном стиле

Для использования нужно обеспечить наличие коллекции **experimentFlag** в стейте
(К примеру через резолвер **resolveExperimentFlagsSync**)

**Example**
```jsx static
<div>
    <RenderIfExperimentDisabled experimentFlagId="all_some_experiment_id">
        Рендерится если пользователь НЕ попал в эксперимент all_some_experiment_id
    </RenderIfExperimentDisabled>

    <RenderIfExperimentDisabled experimentFlagId="all_some_experiment_id" experimentFlagValue="some_experiment_value" >
        Рендерится если пользователь НЕ попал в эксперимент all_some_experiment_id со значение сплита = some_experiment_value 
    </RenderIfExperimentDisabled>
</div>
```
