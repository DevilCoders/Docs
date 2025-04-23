# Сигналы о состоянии объектов

Данные сигналы не будут работать до анонса второго endpoint [https://st.yandex-team.ru/DEPLOY-2045](https://st.yandex-team.ru/DEPLOY-2045)

PodAgent генерирует следующие `ahhh` сигналы для всех объектов внутри пода и для общего состояния пода:

```
ready                   // Готов ли объект к работе 
                        // Например, в случае layer, это означает, что все файлы скачены и произведен import в porto,
                        // в случае workload это означает, что процесс запущен и прошла хоть одна readiness_check проверка (если readiness_check не указан, workload считается ready не зависимо от наличия процесса start)

in_progress             // Происходят ли сейчас какие-то действия с объектом 
                        // Например, скачиваются исходные файлы для layer или собирается rootfs volume для box

failed                  // При сборке объекта/в процессе валидации собранного объекта произошла какая-то ошибка 
                        // Например, поменялась checksum у static_resource, упал start контейнер workload
```

Иными словами, на каждый объект в спеке генерируется 3 дополнительных сигнала.

Из-за лимита на количество сигналов, который равен 2000, при очень большом количестве объектов в спеке часть пользовательских сигналов может не доходить до yasm.

[Обращаем внимание, что это не единственные сигналы, которые отдает pod_agent.](user-sensors.md#limit)

##  Как интерпретировать сигналы {#how_to_interpret}

Каждый сигнал представляет из себя [гистограмму](https://wiki.yandex-team.ru/golovan/userdocs/datatypes/hgram/), в которой заданы 4 интервала: `[0, 1, 2, 3]`

Интервал от 0 до 1 соответствует состоянию `unknown`.
Интервал от 1 до 2 соответствует состоянию `true`.
Интервал от 2 до 3 соответствует состоянию `false`.
Интервал от 3 до `inf` ничему не соответствует, 3 просто является барьерным значением.

Для просмотра состояния сигнала можно воспользоваться фукнцией `hcount(signal, lower, upper)` и сделать, например, [вот такие графики](https://yasm.yandex-team.ru/panel/chegoryu.pod-agent-test-stage/93116049-18b2-4275-eb4a-0f6a63eca0d3/).

Обычно, почти всегда там будут только `true` или `false`.
`unknown` встречается очень редко и, чаще всего, означает, что `pod_agent` еще не приступил к каким-либо действиям с этим объектом.

##  Как удобно смотреть {#how_to_look}

Например, можно воспользоваться [следующей template панелью](https://yasm.yandex-team.ru/template/panel/yd-pod-conditions/prj=pod-agent-test-stage-on-xdc.main-deploy-unit;boxes=TestServiceBox,TestTcpAndCwdBox,TestEnvAndInitBox,TestCustomUserBox;layers=RootFSLayer,TestServiceLayer;static_resources=FileChecker,TestFiles,TestStaticResource;volumes=TestServiceVolume;workloads=TestServiceWorkload,TestTcpAndCwdWorkload,TestEnvWorkload,TestFilesWorkload,TestMultiSecretFilesWorkload,TestWorkloadInitCmdWorkload,TestBoxInitCmdWorkload,TestCustomUserWorkload;show_unknown=false/)

##  Почему некоторые поды могут пропадать {#flap}

Сигналы с `pod_agent` собирает `yasm_agent`, к сожалению, [он перезагружается раз в сутки и при обновлениях](https://st.yandex-team.ru/GOLOVANSUPPORT-1576#5ed634b2dc4d0d3487ae1034), поэтому иногда сигналы могут пропадать на 5-10 секунд.

Пожалуйста, учтите это при настройке ваших алертов.

##  Сигналы с объектов {#objects}

Сигналы с объектов имеют следующий вид:

```
condition_object_<object_type>_<object_id>_<condition_type>_ahhh
```

###  Примеры {#object_examples}

####  Box {#box}

```
condition_object_box_id_ready_ahhh
condition_object_box_id_in_progress_ahhh
condition_object_box_id_failed_ahhh
```

####  Layer {#layer}

```
condition_object_layer_id_ready_ahhh
condition_object_layer_id_in_progress_ahhh
condition_object_layer_id_failed_ahhh
```

####  Static resource {#static_resource}

```
condition_object_static_resource_id_ready_ahhh
condition_object_static_resource_id_in_progress_ahhh
condition_object_static_resource_id_failed_ahhh
```

####  Volume {#volume}

```
condition_object_volume_id_ready_ahhh
condition_object_volume_id_in_progress_ahhh
condition_object_volume_id_failed_ahhh
```

####  Workload {#workload}

```
condition_object_workload_id_ready_ahhh
condition_object_workload_id_in_progress_ahhh
condition_object_workload_id_failed_ahhh
```

##  Сигналы с пода {#pod}

Помимо сигналов с объектов, есть глобальные сигналы со всего пода, имеющие следующее значение:

```
ready = AND (workloads with readiness check ready condition)
in_progress = OR (all objects in_progress condition)
failed = OR (all objects failed condition)
```

Сами значения сигналов вот такие:

```
condition_pod_ready_ahhh
condition_pod_in_progress_ahhh
condition_pod_failed_ahhh
```
