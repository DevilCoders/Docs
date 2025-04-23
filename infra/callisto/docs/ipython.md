## Ipython

**Всякое**
1. ##### Контрольная табличка

    (на примере jupiter pip) – задеплоить что-то на pip и отключить автоматику:
    ```python
    table = user.jupiter.pip.get_yt_target_table(readonly=False)
    table.write(table.target_class(deploy={1636880437}, search=1636880437), lock=False, comment='Force 1636880437')
    ```
    С lock=True таблица будет залочена, её нужно будет разлочить вручную. В большинстве случаев, это не требуется и можно ставить lock=False.

2. ##### Удалить шард из трекера:
    ```python
    tracker = get_tracker('arnold', False)
    to_delete = [res.name for res in tracker.list_resources('/web/prod/1541972782/WebTier0/', 'primus-WebTier0-0-1063-1541972782')]
    tracker.delete_resources('/web/prod/1541972782/WebTier0/', to_delete)
    ```
3. ##### Заоверрайдить выгрузку на быстрых тачках (full_build отключает инкрементальность):
    ```python
    shards = ['primus-WebTier0-0-1222-1539642264']
    for (h, p), cfg in fast_builders.iter_host_port_config(user.jupiter.yt_observers.WebTier0, shards, full_build=True):
        configs.override.override_one(h, p, cfg)
    ```
4. ##### Почистить трекер

    к сожалению, нужно делать достаточно часто. [Мониторинг](https://nda.ya.ru/3UaDYT), [графики](https://nda.ya.ru/t/KLZgrue14iz9nz):
    ```python
    tr_cleaner = get_tracker_cleanup_helper(readonly=False)
    sub_nodes = tr_cleaner.list_sub_nodes('web/prod')
    обязательно смотрим на sub_nodes глазами, что там именно разные поколения баз, а не еще один уровень web/prod/whatever
    for namespace in sub_nodes[:-10]:
        tr_cleaner.remove_node(namespace)
    ```
    еще способ собрать все поколения на удаление, оставив последние 10 в каждом проекте:
    ```
    projects = ['images', 'web', 'video']
    sub_nodes = set()

    for prj in projects:
        candidates = []
        for entity in tr_cleaner.list_sub_nodes(prj):
            entity_name = entity.split('/')[-1]
            if entity_name.startswith('1'):
                candidates.append(entity)
            else:
                newprj = entity.replace(tr_cleaner._yt_root, '').strip('/')
                if newprj not in projects:
                    projects.append(newprj)
        sub_nodes |= set(sorted(candidates)[:-10])
    ```
5. ##### Почистить маппинги rs:
    ```python
    mapping_cleaner = get_mappings_cleanup_helper('web', readonly=False)
    for mapping in mapping_cleaner.list_sub_nodes('vla/WebTier1/mapping/')[:-10]:
        mapping_cleaner.remove_node(mapping)
    ```
6. ##### Изменить конфиги мультибет

    (например веба):
    ```
    table = user.jupiter.multi2.base.get_configs_table(False)
    for slot_id in table.slot_ids():
        table.update_slot_configs(slot_id, mmeta_config='sbr:12345678')
    ```

**Отладка**

1. ##### Провернуть одну итерацию loop:
    ```python
    import infra.callisto.configs.collector as configs_collector
    readonly = True
    registry = root_ctrls.__dict__['<имя корневого контроллера>'] # например registry = root_ctrls.__dict__['video/hamster']
    ctrl = registry.make_ctrl(readonly)
    configs_keeper = configs_collector.ConfigsCollector(registry.configs_storage.get_storage(), readonly)
    context = registry.context_storage.get_storage(readonly)

    loop.do_iteration([ctrl], reports.all, configs_keeper, context)
    ```
