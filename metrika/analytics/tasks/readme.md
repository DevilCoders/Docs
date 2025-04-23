## Tasks

1. Здесь живут ноубуки аналитиков метрики
2. Для простой загрузки тетради в аркадию есть небольшая функция. Она запишет текущий ноутбук в папку `metrika/analytics/tasks`. Если нужно куда-тот вв другое место, то всегда можно запушить руками. Также если такйо файл был, то функция скорее всего не отработает, поэтому рекомендую именовать тетради уникально 
```python
from metr_utils.notebook_to_arcadia import push_notebook_to_arcadia
push_notebook_to_arcadia(commit_message='METR-44444: find missing reports')
```
