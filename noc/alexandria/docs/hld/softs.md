## Soft
**Soft** - это набор информации о конкретном релизе ПО для сетевого оборудования.  
Главной содержательной частью сущности Soft является набор файлов (`Files []SoftFile yaml:"Files"`)


[softs в формате yaml](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/source/soft)

Пример:
```json
Files:
  - 
    FileName: "CE12800-V200R019C10SPC800.cc"
    Type: main
    Version: "V200R019C10SPC800"
    URL: "tftp://noc-myt.yndx.net/"
  - 
    FileName: "CE12800-V200R019SPH007.PAT"
    Type: patch
    Version: "V200R019SPH007"
    URL: "tftp://noc-myt.yndx.net/"
Type: "vrp85"
SWType: "Huawei VRP 8.5"
```

* Files - список объектов типа файл. Файлы имеют типы, на которые могут опираться процедуры установки
* Type(vrp85) - обобщённый тип, сейчас отражает breed из Racktables. Нужен для парсинга ПО на устройствах.
* SWType - аттрибут SW Type из Racktables. Обозначает принадлежность к взаимозаменяемому ПО.