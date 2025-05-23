# Иерархия сущностей

![Иерархия выглядит следующим образом](../_assets/concepts/entity-hierarchy/entity-hierarchy.png)

На нижнем уровне этой логической группировки находятся поды.

Поды состоят из одного или нескольких Box'ов. При этом боксы могут быть как пользовательскими (в них выполняется пользовательский код), так и инфраструктурными (например, если пользователю нужно включить поставку логов stderr/stdout, то в поде будет создан инфраструктурный Box с PushAgent).

Внутри каждого бокса может находиться один или несколько workload'ов.

## Сущности {#entity}

**Project** - сущность высокого уровня, используемая для объединения Stage'ей одного сервиса. На этом уровне определяется, квота какого из сервисов будет использована для запуска сервиса. Например, в один проект могут входить 3 стейджа для фронтенда (test/pre/prod) и 3 стейджа для бэкенда (test/pre/prod).

**Stage** - логическое объединение Deploy Unit'ов, которые должны оркестрированно выкатываться. Все stages живут в одном общем неймспейсе (не стоит называть стейджи слишком "общими" именами).

**Deploy Unit** - группировка **одинаковых** подов, созданная на основе определенного примитива деплоя.

**Pod** - единица планирования на кластере. Т.е. планировщик решает задачу размещения нужного вам количества подов на машинах кластера с учетом указанных вами ограничений.



