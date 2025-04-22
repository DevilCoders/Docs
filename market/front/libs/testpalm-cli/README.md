# testpalm-cli

Утилита для получения количества тесткейсов в статусах. 

<img src="screenshots/screenshot1.png" width="500"/>

> В перспективе утилита научится получать другие 
  интересные выборки данных из TestPalm 


## Install

```bash
npm i git://github.yandex-team.ru/extg/testpalm-cli#v0.0.4 -D
```


## Usage

```bash
testpalm-cli vendor_auto
{
  "total": 713,
  "is_autotest": 157,
  "automated": 120,
  "actual": 415,
  "archived": 131,
  "needs_changes": 10,
  "automation_in_progress": 11,
  "duplicate": 9,
  "needs_repair": 8,
  "on_review": 9
}
```


### Post to Statface

Для того чтобы отправлять данные в [Stateface](https://stat.yandex-team.ru) с
рабочей машины нужно указать переменную окружения `STATFACE_API_TOKEN`. 
[**Получить токен можно тут**](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=801af94c94e040848ebe206086a7a4e2)

`--statface`, `-s` --  путь к отчету. Должен включать проект и путь внутри проекта.


#### Примеры вызовов

`testpalm-cli vendor_auto --statface Market_Vendors/CodeHealth/TestPalmCoverage` 
**- отправка данных в Statface**

<img src="screenshots/screenshot2.png" width="500"/>

`testpalm-cli vendor_auto --s Market_Vendors/CodeHealth/TestPalmCoverage -v` 
**- вывод и отправка данных в Statface**

<img src="screenshots/screenshot3.png" width="500"/>

--- 

**TODO:** 
- [ ] Может стоит прокидывать и другие параметры отсюда 
  https://wiki.yandex-team.ru/statbox/Statface/externalreports/#zagruzkadannyx
