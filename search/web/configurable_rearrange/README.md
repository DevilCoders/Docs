## Configurable rearrange
Это простая библиотека для модификации поведения переранжирований в рантайме (для метапоиска веба).
Назначения:
1. Поддерживать экспы с модификаций переранжирований. Основной пример - бусты (и пессимизации) документов.
2. Быть пригодной для выкатки принятых изменений.
3. Выкатывать экспы и релизы без приёмок среднего.
4. Поддерживать множество экспов в различных измерениях.

## Применение патчей на графы
1. Патчи через параметры - исключение для снятия серпов. Экспы не должны кататься с патчами в параметрах, только с именами
2. Для детерменированности наложения нескольких патчей:
* сначала применяются все удаления
* потом все добавления
* любые колизии считаются ошибкой и патчи не применяются

## Как раскладывать файлы:
Рекомендуется следующий способ:
1. в configs/patches завести файлик my_exp_bundle.proto.txt
2. добавлять туда все нужные вариации графов и патчей в неймспейсе "my_exp"
3. рекомендуется во все патчи и графы прикладывать результаты визуализации

## Как выкатывать
1. обновить TrunkGraph
2. протестировать его MIDDLE-375
3. отвести в веткой releases_archive_bundle.proto.txt
4. завести новый рулсет в search/formula_chooser отведением от транка
5. добавить новый маппинг
6. пройти процедуру выкатки маппингов из search/formula_chooser

## Визуализация и разработка графов и патчей
Смотри [MIDDLE-415](https://st.yandex-team.ru/MIDDLE-415) или ссылки на yql запросы в прод-графах

## Соглашения:
1. Фетч-фактор ноды должны иметь приоритет = 1
2. Максимальный приоритет нод в графах имеет порядок сотни
3. Шаг между приоритетами для системных графов - десятки

## Управление через cgi

Параметры без доп-пометок **не предназначены для экспов**..

1. Отладить граф <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/DebugMarkers=1```.<br/>
В этом режиме будут добавлены очень многословные маркеры. Более того - их порядок не будет естественным.
1. Выбрать базовы граф для применения <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/ForceGraphName=1```.<br/>
Для RearrsConf: <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/ForceRearrsConfGraphName=1```
1. Задать базовы граф для применения: <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/Base64ProtoTextGraph=data```, <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/Base64ProtoBinaryGraph=data``` (бинарный формат). <br/>
Для RearrsConf: <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/Base64ProtoTextGraphRearrsConf=data```, <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/Base64ProtoBinaryGraphRearrsConf=data``` (бинарный формат). <br/>
1. Задать патч для применения <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/Base64ProtoTextPatch=data```, <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/Base64ProtoBinaryPatch=data``` (бинарный формат). <br/>
Для RearrsConf: <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/Base64ProtoTextPatchRearrsConf=data```, <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/Base64ProtoBinaryPatchRearrsConf=data``` (бинарный формат). <br/>
1. Задать патч для применения <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/ApplyPatchesByName/NamespaceName=PatchName```. **Разрешено в абт**.
1. Задать патч для применения в RearrsConf <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/ApplyPatchesByNameForRearrsConf/NamespaceName=PatchName```. **Разрешено в абт**.
1. Создать и добавить патч, меняющий значение ноды c типом SetConstant/IfGreater/IfLower (делает += к Value)<br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/DynamicPatch/Namespace/MyNodeName=-1000```. **Разрешено в абт**.
1. Создать и добавить патч, меняющий значение ноды в RearrsConf c типом SetConstant/IfGreater/IfLower (делает += к Value) <br/>
```&rearr=scheme_Local/ConfigurableRearrangeApplier/DynamicPatchForRearrsConf/Namespace/MyNodeName=-1000```. **Разрешено в абт**. <br/>

(Пример udf для кодирования графов и патчей в base64 и обратно: https://yql.yandex-team.ru/Operations/YZal-JfFt1sCkKPeZqX-rg9MlY-Lh7JRNgBH3MCcfEY=)


## 2. Графы в рантайме

## 2.1 Прс-ный граф-конфигуратор

* Работает на всё прс, имеет возможность считать статистики факторов по прс-у (not implemented).
* Имеет возможность пробрасывать параметры в последующие графы.
* Имеет возможность пробрасывать опции (LocalScheme) в другие переранжирования.

**NOTE**: проброс опций в другие переранжирования
* не сработает если переранжирование выполнится после.
* работает только если соответствующая опция нигде не выставлена

Чтобы отключить набор опций в конфигураторе нужно 
* или удалить ребро в маркер-ноду
* или удалить ребро в маркер-ноду
* или добавиться того чтобы значение ноды было 0

## 2.2 Подокументный граф бустов

## 3. MergeWithNodesAndEdgesFromGraphsAtBuildStage - наследование графов

- Для тех случаев когда часть графов дублируется в нескольких местах, может быть удобен механизм MergeWithNodesAndEdgesFromGraphsAtBuildStage
- Этот механизм поддержан только и исключительно при построении графов для экспорта (то есть секция будет проигнорирована или приведёт к ошибка в любых тулзах или рантаймах)
- Работает аналогично тому что все Nodes/Edges секции были бы скопированы из реципиента в граф, в котором указана MergeWithNodesAndEdgesFromGraphsAtBuildStage (доп логики про разрешение конфликтов нет)
- Секция работает в том числе рекурсивно, но циклы запрещены
- Нельзя инклудить транк графы в транк графы (иначе будет незаметный зеро-дифф) - используйте схему с DuplicateAtBuildStageAsGraphName и ссылки на конкретные версии


## 4. Создание новой версии релизного графа
Для удобства отслеживания истории используем следующую схему:
1. есть trunk граф для каждого логического типа
2. в рулсетах указываются только их релизные версии
3. для того чтобы не держать в транке 2 одинаковых версии есть механизм DuplicateAtBuildStageAsGraphName
4. при изменение любого trunk графа нужно сначала
  - скопировать (arc/svn cp) в releases_archive
  - прописать в ya.make новый файл
  - поменять имя и удалить секцию DuplicateAtBuildStageAsGraphName
  - теперь можно менять основной граф (и конечно имя в DuplicateAtBuildStageAsGraphName)


5. Если граф является базовым (через механизм MergeWithNodesAndEdgesFromGraphsAtBuildStage) - то придётся также сделать новые версии зависимых графов и прокатить маппинг с этим изменением
6. В ряде случаев можно вносить inplace изменения без заведения веток для всего: если это безопасное зеродифф включение новой логики
 - при этом всегда могут возникнуть performance проблемы в релизе
 - для таких случаев обязательно следует предупреждать дежурного по релизам архивов

Пример ревью, в котором должно быть всё понятно: https://a.yandex-team.ru/review/2298093

1. arc cp trunk-graph-path.proto.txt release_archive/old_released_name.proto.txt
2. 2 строчки изменение в old_released_name.proto.txt
3. логические изменения trunk-graph-path.proto.txt + обновление имени + обновление визуализации
4. изменение в mappings.proto.txt
