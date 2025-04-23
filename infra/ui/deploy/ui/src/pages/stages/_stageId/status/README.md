## Настройки пересчёта
Чтобы увидеть скрытые настройки, нужно выставить флаг `status-view-settings-visible` в localStorage.
```javascript
localStorage.setItem('status-view-settings-visible', true);
```

## Схема хранения StatusView моделей
```mermaid
graph TD
   UI -- Effect trigger --> useStatusViewUpdate
   useStatusViewUpdate -- React Context Callback --> Store
   Store -- React Context --> use*StatusView
   use*StatusView --> UI
```

## useStatusViewUpdate
Процесс обновления дерева
Зеленые узлы — активная часть дерева
Оранжевые узлы — расчитывались в предыдущие разы
Остальные не расчитывались

В рамки сгруппированны узлы, видимые на странице (например DeployUnit1 хоть и не выбран, но присутствует в общем списке)
```mermaid
graph TD
   stage --> deployUnit1
   stage --> deployUnit2
   stage --> deployUnit3

   subgraph du
      deployUnit1
      deployUnit2
      deployUnit3
   end

   deployUnit1 ---> deployUnit1Tree...

   deployUnit2 ---> replicaSet_Sas
   deployUnit2 ---> replicaSet_Vla
   deployUnit2 ---> replicaSet_Man

   deployUnit3 ---> deployUnit3Tree...

   subgraph rs
      replicaSet_Sas
      replicaSet_Vla
      replicaSet_Man
   end

   replicaSet_Sas ---> replicaSet_SasPods...

   replicaSet_Vla ---> Pod1
   replicaSet_Vla ---> Pod2

   replicaSet_Man ---> replicaSet_ManPods...

   subgraph pods
      Pod1
      Pod2
   end

   style stage fill:green,color:white
   style deployUnit2 fill:green,color:white
   style replicaSet_Vla fill:green,color:white
   style Pod1 fill:green,color:white
   style Pod2 fill:green,color:white

   style deployUnit3 fill:orange
   style replicaSet_Sas fill:orange

```

Процесс вычисления и сохранения моделей
1. Взять из redux данные для объектов в рамках (данные стейджа, всех деплой-юнитов, всех реплика-сетов для активного юнита и все поды в активной локации для юнита)
1. Вычисления снизу вверх, сначала поды, потом rs, потом du, потом стейдж
1. Для зелёных объектов брать данные из redux
1. Для оранжевых объектов смотреть время последнего обновления - если меньше ttl, брать кэш из контекста, если больше, стирать данные из контекста и брать пустые массивы
1. Для остальных объектов брать пустые массивы
1. Все вычисленные объекты записать в контекст

Таким образом покрываются все текущие сценарии — то есть все объекты на странице получают свою StatusView модель. Если изменится вёрстка — например будут видны все реплика-сеты в дереве с деплой-юнитами, то необходимо будет обработать большую часть дерева, в данном случае рассчитать все реплика-сеты у всех деплой-юнитов, но для этого нужны изменения и в redux части, ведь rs надо сначала скачать по сети.
