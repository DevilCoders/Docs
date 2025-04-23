# Rearrange Formulas Bundle
---

### <a name="archives"> Где хранится информация о формулах для архива</a>

- **Middle:** https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearr_formulas_bundle/content  
- **Base:** https://a.yandex-team.ru/arc/trunk/arcadia/search/runtime_archives/base_search/formulas
- **L1:** https://a.yandex-team.ru/arc/trunk/arcadia/search/runtime_archives/l1/formulas

 ### Файлы
- common_config.proto.txt - конфиг с общими параметрами
- Остальное:  
    **а) файлы формул** (L3Relev, L4Pers, ProximaPredict и т.п) - содержат и ProdFormula, и ExperimentPack  
    **б) персональные файлы c экспериментами** (_exps.proto.txt) - только ExperimentPack, но с указанием в какие файлы формул вмержить на этапе сборки архива, и с отдельной выделенной квотой (владельцы разных квот, больше не конфликтуют за место в архиве)

---
## Кубик RearrFormulasBundle:Commit

Коммит формул осуществляется этим кубиком: https://nirvana.yandex-team.ru/alias/operation/rearrformulasbundlecommit

#### **Input:**
- **FmlFormulas** [1..∞] (JSON, FML Formula)

#### **Options:**
- **Ticket**
- **ArchiveType** - тип архива, в который должны попасть формулы
- **FileToUpdate** - имя файла в [соответствующем архиве](#archives)
- **FormulaNamesToApply** - необходимо для персональных файлов с экспами (_exps.proto.txt). Указываются назвния файлов с формулами, куда включить expPack на этапе сборки (например: "L3Relev", "L4Pers").
- **DaysForExpiration** 
- **DryRun** (DoNotMerge)

---
## Персональные файлы c экспериментами
Их можно завести самостоятельно, выделив себе отдельную квоту в архиве. 
Таким образом коммиты формул в другие квоты, не скажутся на вашу возможность добавлять формулы в личную квоту  

Сейчас есть огрничения только на суммарный размер всех квот в архиве (ограниние задано в common_config)

Чтобы выделить квоту нужно в [соответствующем месте](#archives) завести нужный файл: 
**personal_{login}_exps.proto.txt** или  
**project_{name}_exps.proto.txt**
```
ProjectOrLogin: "{ProjectOrLogin}"
Description: "its optional field"
AllowedExpFormulasSizeMb: 100

```
и добавить в **ya.make**

## Состояние квот и причины падений/ошибок

Подробный лог можно найти так:  
-> Перейти внутрь композитного кубика коммита  
-> Найти кубик _CommitExpFormulasToRearrBundles:SbWrapper_
-> Открыть лог _executor.err_  

По этому логу можно определить заполненность и состояние каждой квоты и общую занятость в архиве, в который происходил коммит , а также причину падения в случае таковой

##### Безопасное удаление
При оченищении своей квоты тесты
```
ya t ~/arc/arcadia/search/web/rearr_formulas_bundle/content_io_lib/ut/ 
```
проверят, что по прежнему присутствуют формулы из маппингов и не были удалены формулы, которые бегут в текущих экспах.
А также выведет новую статистику по квотам

---
## Ручное добавление формул
Можно добавить вручную в нужные файлы и дождаться всех unit-тестов  
  
Более быстрый способ:  
Скипт https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearr_formulas_bundle/formulas_bundle_ops/mode_add_formulas.cpp

Пример как запустить:
```
ya make ~/arc/arcadia/search/web/rearr_formulas_bundle/formulas_bundle_ops/ && \
 ~/arc/arcadia/search/web/rearr_formulas_bundle/formulas_bundle_ops/formulas_bundle_ops append_formulas \
'{ArchiveType="Middle"; \
FileToUpdate="personal_login_exps.proto.txt"; \
Owner="login"; \
Ticket="xxx-111"; \
ArcBinPath="./arc"; \
FmlIds=["810123"]; \
FormulaNamesToApply=["L3Relev";"L4Pers"]; \
CommiterUser="login"}'
```

## Смотреть свойства формул
https://domains.yandex-team.ru/domain/fml/formula/42816
https://fml.yandex-team.ru/formula/856596
