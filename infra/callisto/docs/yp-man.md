##### Контуры web-поиска в YP

**Главное правило**: ничего нельзя менять через интерфейс deploy!
Иначе stage controller перетрёт необходимые настройки и всё взорвётся в одну секунду.

###### Prod Stage в сожительстве в man
Группы сожительства: MAN_YP_COHABITATION_PLATINUM_BASE (один инстанс на хост).
https://deploy.yandex-team.ru/project/man-web-search

В **шаблон репликасета** нужно дописать:
```yaml
      replica_set:
        replica_set_template:
          pod_template_spec:
            annotations:
              pod.rbind.basesearch: true          # чтобы правильно смонтировался /basesearch, step 1
            labels:
              yd.enable_enumerated_pod_ids: true  # пронумерованные идентификаторы подов
              yd.disable_pods_move: true          # запретить перенос подов
              yd.node_segment_id: base-search     # или base-search-cohabitation, наш сегмент
            spec:
              enable_scheduling: false            # совсем запретить перенос подов
              host_name_kind: persistent          # иначе у подов будут слишком длинные fqdn, сломается porto
              dynamic_attributes:
                annotations:
                - pod.rbind.basesearch            # чтобы правильно смонтировался /basesearch, step 2
```

###### Вспомогательные сервисы в няне
https://nanny.yandex-team.ru/ui/#/services/catalog/man_cohabitation_deploy/
https://nanny.yandex-team.ru/ui/#/services/catalog/man-web-base-resources/

###### Потребные слои и ресурсы
- Каталог /basesearch: https://sandbox.yandex-team.ru/resource/1193357615/view
- Callisto agent: https://sandbox.yandex-team.ru/resource/1133249188/view


###### Переход на scheduling hints
1) прописать scheduling_hint

получаем список подов подсете:
имя подсета формируется как {/meta/id}.{/spec/deploy_units/<deploy_unit_name>} из спеки деплоя
```
ya tool yp select pod --address man-pre --filter "[/meta/pod_set_id]='<pod_set_id>'" --selector /meta/id
```
для каждого пода получаем его текущее размещение:
```
ya tool yp get pod <pod_id> --address man-pre --selector /spec/node_id
```
прописываем текущее размещение в scheduling hints:
```
ya tool yp update --address man-pre pod <pod_id> --set /spec/scheduling/hints "[{node_id=\"<node_id>\"; strong=%true}]"
```

2) включаем работу планировщика

Для этого нужно включить /spec/deploy_units/<deploy_unit_name>/replica_set/replica_set_template/pod_template_spec/spec/enable_scheduling (false -> true) в спеке деплоя

3) для теста можно снять под с ноды:
```
ya tool yp evict-pod --address man-pre <pod_id>
```
если все сделано правильно планировщик приземлит под на ту же ноду, что прописана в scheduling hints


###### Изменение размера volume
1) Изменение размера:
В спеке деплоя меняем /spec/deploy_units/<deploy_unit_name>/replica_set/replica_set_template/pod_template_spec/spec/disk_volume_requests[id=<volume_id>]/quota_policy/capacity
Утверждается так же, что при этом обязательно требуется изменение id самого volume. Так как этот id более нигде не участвует - меняем

2) Для материализации изменений требуется перепланирование пода, например с помощью снятия пода с ноды:
```
ya tool yp evict-pod --address man-pre <pod_id>
```

###### Аналог max degrade speed в deploy
Настраивается на каждый deploy unit с помощью ya tool yp. Для этого на соответствующем replica_set-е
вывешивает метка yd.deploy_speed:

```
ya tool yp update replica_set web-search-test.tier1-base --set /labels/yd.deploy_speed '{"update_portion"=4;"min_delay"=75;}' --address man-pre
```

update_portion - порция подов (шт), которые могут уйти в 1 итерацию replica set controller-а (RSC)
min_delay - минимальная задержка (сек) между выводами порций подов

если RSC крутится быстрее чем min_delay то в каждые min_delay сек (с округлением вверх по итерациям) он будет выводить по update_portion подов
если RSC крутится медленнее чем min_delay то в каждую итерацию (сколько бы она не заняла) будет выведено update_portion подов

На текущий момент частота итераций RSC составляет 1 / (50-80 секунд), разнится от локации к локации

Общее кол-во выведенных подов ограничивается сверху через max_unavailable
