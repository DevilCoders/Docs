## Именование балансеров

```
Production:
{Datacenter}{Building}-{Module}{TYPE}{NumericID}{LetterID}.yndx.net

Hypervisor (TYPE="kvm"):
{Datacenter}{Building}-{Module}{TYPE}{NumericID}{LetterID}.yndx.net

VM:
{Datacenter}{Building}-{Module}{TYPE}{NumericID}{LetterID}.{PROJECT}-{ENVIRONMENT}.yndx.net

TYPE = {
  "lb",
  "lbchecker", # проверка конфигурации keepalived
  "kvm",
}

PROJECT = {
  "l3mgr",
  "rtnmgr",
}

ENVIRONMENT = {
  "unstable",
  "test",
  "rc",
  "prestable",
  "stable"
}

REGEX:
* Datacenter: /[a-z]+/
* Building: /[0-9]*/
* Module: /[0-9]*/
* NumericID: /[0-9]+/
* LetterID: /[a-z]+/
```

## Балансерные теги

Описание балансерных тегов в racktables:
- stages (оно же environment) уже заведены в RT

```
STAGE = {
  "unstable",
  "testing",
  "prestable",
  "stable"
}
```

- назначение балансеров — тег `balancer-{TYPE}`, где

```
TYPE = {
  "common",   # основной набор балансеров
  "project",  # балансировщик в проектных сетях
  "nat",      # балансеры с NAT сервисами PCIDSS и OFD
  "checker",  # балансеры для тестирования конфигураций
  "cdn",      # региональные балансеры
  "cloud",    # балансеры для Яндекс.Облака
  "blocking", # балансеры для схемы обхода блокировок, текущие UA балансировщики
  "awapsftp", # единственные в своем роде балансеры в проектных сетях с катомными правилами файрвола
}
```

Всё это экспортируется в кондуктор по группам `l3-balancers-{TYPE}-{STAGE}`  и входит в группу l3-balancers.
