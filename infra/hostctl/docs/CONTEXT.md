# Context
В рендеринге можно использовать переменные вычисленные на основе `host_info`.
При их вычислении используется язык выражений [cel-go](https://github.com/google/cel-go).
```
/* Context to be evaluated on from host info
   and applied (interpolated) to spec. */
message Context {
    message Match {
        string exp = 1; // cel-go like expression, yields boolean
        string val = 2; // String value to be used if expression evaluated to true
    }
    /* Variable definition via match */
    message Var {
        string name = 1;
        repeated Match match = 2;
    }
    repeated Var vars = 2;
}
```
В каждом `exp` объявляем выражение возвращающее bool `<some_expr> -> bool`.
В переменную подставляется первое совпавшее значение. Если не совпало ни одно, подставляется пустая строка.

В выражениях можно использовать функции [source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/engine/hostctx/funcs/funcs.go):
* `has_tag(<walle_tag>)`
* `has_group(<gencfg_tag>)`
* `geo(<location>)`
* `focal()` <=> `os_codename == 'focal'`
* `xenial()` <=> `os_codename == 'xenial'`
* `prestable()` <=> `has_tag('rtc.stage-prestable')`
* `production()` <=> `has_tag('rtc.stage-production')`
* `prj(<walle-project>)`
* `perc(<server_num>)` - может использоваться для выкладки на проценты
* `h(<hostname>)` - поддерживается полный и сокращенный формат e.g. `h('sas1-5166')`, `h('sas1-5166.search.yandex.net')`
* `switch(<switch-id>)`
* `dc_queue('<queue_name>')` or `dc_queue(['<queue1>', '<queue2>', ..., '<queueN>'])` - аналог grains.walle_queue (короткое имя очереди ДЦ из wall-e)

Переменные:
* доступные всегда
  * `hostname string`
  * `num int`
  * `mem_total_gib`
  * `walle_project string`
  * `walle_tags []string`
  * `net_switch string`
  * `gencfg_groups []string`
  * `location string`
  * `dc string`
  * `dc_queue string` - аналог grains.walle_queue (короткое имя очереди ДЦ из wall-e)
  * `kernel.major int` при неудачном парсинге как int значением выставляется -1
  * `kernel.minor int` при неудачном парсинге как int значением выставляется -1
  * `kernel.build int` при неудачном парсинге как int значением выставляется -1
  * `kernel.patch int` при неудачном парсинге как int значением выставляется -1
  * `kernel.release string` строка вида `'4.19.119-30.1'`
  * `os_codename`
  * `cpu_model string` строка вида `AMD EPYC 7662 64-Core Processor`
* вычисленные на предыдущих шагах

Примеры:
  * kernel.major == 4
  * kernel.minor >= 19

Объявление переменной ver: e.g
```
vars:
  - name: "ver"
    match:
      - exp: has_tag('rtc.stage-prestable')
        val: "2.440-20200723"
      - exp: geo('sas')
        val: "2.440-20200723"
      - exp: geo('vla')
        val: "2.440-20200723"
      - exp: geo('man')
        val: "2.440-20200723"
      - exp: geo('msk')
        val: "2.440-20200723"
```

Переменные в `spec` и `meta` шаблонизируются через `{}`
e.g.
```
meta:
  annotations:
    stage: "{location}"
```

P.S: некая особенность yaml парсинга: `!` - спецсимвол, `- exp: !has_tag('qloud')` распарсится как `- exp: ''`, exp с ! следует оборачивать в ковычки  `- exp: "!has_tag('qloud')"`
