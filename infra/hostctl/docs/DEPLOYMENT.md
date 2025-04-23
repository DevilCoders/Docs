# Deployment

## Хранение спек

### Хранить спеки в аркадии в формате: 
*best practices*
* Если спеки отличаются в зависимости от локации
    * [prestable-yandex-packages.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/yandex-packages/prestable-yandex-packages.yaml)
    * [sas-yandex-packages.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/yandex-packages/sas-yandex-packages.yaml)
    * [vla-yandex-packages.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/yandex-packages/vla-yandex-packages.yaml)
    * [man-yandex-packages.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/yandex-packages/man-yandex-packages.yaml)
    * [msk-yandex-packages.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/yandex-packages/msk-yandex-packages.yaml)
* Если у нас всегда выкладывается одна гомогенная версия на все локации 
    * [yandex-hm-reporter.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/yandex-hm-reporter.yaml)

### Создание релизных ПРов из аркадии [hmctl](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/hmctl)

Если спеки хранятся в аркадии, то можно воспользоваться hmctl для создания релизных ПРов. 
* Если в имени спеки присутствует префикc локации (<prestable | sas | vla | man | msk>). То создаем PR вот так

    `hmctl push <location>-yandex-packages.yaml -r <core|sysdev|etc...> -m 'deploy yandex-packages'`
* Если префикса в имени файла нет, то указываем `-c <location>` из cmdline

    `hmctl push yandex-hm-reporter.yaml -r <core|sysdev|etc...> -c <location> -m 'deploy yandex-hm-reporter'`

### Выкладка новой версии по процентам
Размечаем по стейджам выражением из `stage`. Стейджи не должны меняться при выкладке версии на другие проценты.

Далее для каждого из стейджей прописываем версию, которую хотим выложить.

В примере ниже мы выложим версию `0.1-7935023` на 10% стейджа yt и на 50% стейджа stable. На остальные хосты приедет версия 0.1-7818114. 

**Важно!**
Порядок выражений важен. Выражения выполняются по порядку прописаному в yaml. В результат вычисления попадет val из первого выполнившегося с True выражения из exp.
```yaml
vars:
  - name: "stage"
    match:
      - exp: "has_tag('yt')"
        vla: "yt"
      - exp: "default()"
        val: "stable"
  - name: "ver"
    match:
      - exp: "stage == 'yt' && perc(10)"
        val: "0.1-7935023"
      - exp: "stage == 'yt'"
        val: "0.1-7818114"
      - exp: "stage == 'stable' && perc(50)"
        val: "0.1-7935023"
      - exp: "stage == 'stable'"
        val: "0.1-7818114"
```
