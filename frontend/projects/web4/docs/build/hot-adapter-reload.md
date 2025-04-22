# Hot Adapter Reload (при локальной разработке)

Что бы не перезапускать Report Renderer после каждой правки, taburet умеет "на лету" перезагружать код модулей, из следующих директорий:
- src/features/**
- src/experiments/**
- src/components/**

Для модулей, которые используются в самом taburet, остается soft-restart RR, т.к. мы не можем делать для них hot reload:
- src/vendors/**
- src/lib/**

[Исходный код](../../src/vendors/taburet/Registry/hotAdapterReload.ts)

----

Если возникают проблемы с Hot Reload, вы можете отключить эту функциональность:
```bash
DISABLE_ADAPTER_HOT_RELOAD=1 npm run dev
```
