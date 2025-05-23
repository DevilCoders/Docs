# Танк для нагрузочного тестирования SPIRIT

Репо хранит настройки для работы танка. Сам танк может быть использован из `Y.Deploy`,
либо из `Sandbox`

При работе танк использует `pandora` в качестве движка.

## Тестовые сценарии

Выбор сценария работы зависит исключительно от патронов. В патроне есть метка `tag`,
определяющая сценарий работы и в поле `patron` лежат данные для данного сценария. Движок пандора
берет патроны из файла `ammo.json`.
Таким образом, для смены сценария работы нужно положить файл патронов
соответствующего сценария рядом с движком под именем `ammo.json` и нужно сменить в конфиге танка
описание стрельбы, оператора, по желанию номер задачи (например можно через опцию старта танка
```bash
yandex-tank  -o "uploader.job_name=Spirit Load Test Scenario" -o "uploader.operator=login" -p "uploader.task=SPIRIT-2214"
```
)

Приготовленные тестовые сценарии генерируются скриптом `ammo.py` (о генерации `python ammo.py -h`)
Конфигурация танка и движка пандоры лежит в файле `tank_conf.yaml`.  
Конфигурация пандоры включена в состав конфига танка (из-за ограничения `Firestarter`,
он не умеет подгружать конфиг пандоры из другого файла)

### DsWsCheckrendererReceipt
Cценарий выполняет следующие действия:
- Пробить чек в `whitespirit`
- Если ок, то передать результат в `darkspirit` (при этом `darkspirit`
  попытается сохранить чек в `loadmock`, и сохранит его в `db`)
- Если ок, распарсить данные для рендера чека по `URL` и
  запросить соответствующие данные у `check-renderer` (при этом `check-renderer`
  запросит чек у `darkspirit`, который возьмет его из `loadmock`)

### CheckrendererPOST
Cценарий выполняет следующие действия:
- Запрос `POST` в рендерилку для рендера чека по передаваемым данным (без похода в другие машины)

### CheckrendererGet
Cценарий выполняет следующие действия:
- Запрос `GET` в рендерилку для рендера чека по номеру фискального накопителя, чека и фискального
признака (с походом в `darkspirit` и `loadmock`)

### DsReceipt
Cценарий выполняет следующие действия:
- Передает чек в `darkspirit` (с походом в `loadmock`)
В данном сценарии важно, чтобы серийный номер фискального накопителя был в БД, а `id`
всех патронов отсустствовали в БД! Иначе DS будет делать на 1 запрос меньше к БД

### WsReceipt
Cценарий выполняет следующие действия:
- Передает чек в `whitespirit`

## Pandora

Подробнее о пандоре [тут](https://wiki.yandex-team.ru/Load/Pandora/#delivery)
и [тут](https://github.com/yandex/pandora)
Код движка указан в `gun.go`
Движок конфигурируется в файлах:
- `tank_conf.yaml` - общие настройки движка, включая адреса мишеней, и профиль стрельб
- `ammo.json` - патроны для стрельб, содержит тип выстрела (сценарий и сам патрон)

### Сборка
Для сборки движка в исполняемый файл необходимо из папки c go кодом выполнить
```bash
ya make
```
Рельтатом будет бинарный файл `spirit_gun` в текущей директории.

### Запуск
Для отладки пандору можно запустить без танка. Для этого нужно вынести конфигурацию пандоры
из конфига танка в отдельный файл и поместить файл движка, конфиг
пандоры и файл патронов под именем `ammo.json` в одну папку и выполнить команду
```bash
./spirit_gun pandora_conf.yaml
```

## Танк
 Для работы танка у машины с танком должны быть все необходимые доступы, в частности
 к мишеням и [инфраструктуре стрельб](https://wiki.yandex-team.ru/Load/howto/idm-puncher/)

 Для работы с танком необходим собранный модуль пушки пандоры и все необходимые для ее работы
 файлы, а также конфиг танка. Поместить все файлы в одну папку и запустить

 Конфиг танка - `tank_conf.yaml`

### Как собрать все конфиги и патроны в одну папку

#### cp/scp
Непосредственно скопировать через cp/scp (при использовании на своем танке)

#### Через `sandbox`/`PandoraResources`
Загрузить файл патронов и исполняемый файл пушки в `sandbox`

Для загрузки файлов под группой `PAYPLATFORM` на 7 дней (604800 в секундах)
```bash
ya upload config/ammo/ammo_CheckrendererPost.json -T AMMO_FILE --owner PAYPLATFORM --ttl 604800 -d 'CheckrendererPost ammo file'
ya upload config/ammo/ammo_WsDsCheckrendererReceipt.json -T AMMO_FILE --owner PAYPLATFORM --ttl 604800 -d 'WsDsCheckrendererReceipt ammo file'
ya upload spirit_gun -T PANDORA_EXECUTABLE --owner PAYPLATFORM --ttl 604800 -d 'Spirit load tests pandora gun'
```
Прописать в конфиге танка загрузку ресурсов с `sandbox` (смотреть комментарий в конфиге танка)

#### Через `sandbox`/`TankShellExec`

Загрузить файлы в sandbox (см выше)

```bash
yandex-tank -c tank_conf.yaml -o "shellexec.prepare=curl https://proxy.sandbox.yandex-team.ru/2388895252 --output ammo.json"
```
Данным способом можно подменять файлы непосредственно при запуске танка без изменения конфига

### Запуск танка

#### Из консоли машины с [танком](https://yandextank.readthedocs.io/en/latest/)

```bash
yandex-tank -c tank_conf.yaml
```

#### Удаленно через [tankapi-cmd](https://wiki.yandex-team.ru/load/lunapark/dev/api/tank/?from=%2FNagruzochnoeTestirovanie%2FLunaPark%2Fdev%2Fapi%2Ftank%2F)

```bash
tankapi-cmd -t tank.6di27wu6w2tu3lr7.sas.yp-c.yandex.net -f ammo.json -f spirit_gun -c tank_conf.yaml -j ./jobno.txt
```

#### Через sandbox

 - Создать в sandbox таску с типом `FIRESTARTER`
 - Выставить группу и описание
 - Скопировать конфиг танка в соответствующее поле
 - Убедиться, что в конфиге танка путь к пандоре указан ссылкой ны sandbox, а патроны
доставляются как ресурсы (см `Как собрать все конфиги и патроны в одну папку`)
 - Запустить таску
