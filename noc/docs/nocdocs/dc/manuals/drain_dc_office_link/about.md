# Как увести трафик с плеча Border-Office

Автор: 
- [Максим Карякин](https://staff.yandex-team.ru/karyakin)

----------

Стоит оговориться что это актуально только для вдуногих и т.д ногих офисов.
Данный способ дрэйна справедлив для таких устройств как:
- `{свитч агрегации}`
- `{VPN-концентратор}`
- `{router for office}`

Вешаем тэг "нагрузка снята" на линковую сеть с офисом и катим аннушкой конфиг на бордер, при этом должен выкатиться примерно следующий конфиг:

```diff
+   policy-statement DRAIN {
+       then {
+           metric add 50000;
+           preference add 1000;
+       }
+   }
[edit protocols bgp group OfficeRouters neighbor 37.9.96.113]
+     import [ DRAIN PE_IMPORT_OFFICE ];
+     export [ DRAIN PE_EXPORT_OFFICE ];
[edit protocols bgp group OfficeRouters neighbor 37.9.96.114]
+     import [ DRAIN PE_IMPORT_OFFICE ];
+     export [ DRAIN PE_EXPORT_OFFICE ];
[edit protocols bgp group OfficeRoutersv6 neighbor 2a02:6b8:0:370b::2]
+     import [ DRAIN PE_IMPORT_OFFICE ];
+     export [ DRAIN PE_EXPORT_OFFICE ];
[edit protocols bgp group OfficeRoutersv6 neighbor 2a02:6b8:0:370b::3]
+     import [ DRAIN PE_IMPORT_OFFICE ];
+     export [ DRAIN PE_EXPORT_OFFICE ];
```
