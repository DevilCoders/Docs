# Как откатить Fast-Data?
## Rollback
1. Заходим в нужный CI-проект: [Fast Data release to WEB](https://a.yandex-team.ru/projects/upper/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast&id=fast-data-web-release), [Fast Data release to VIDEO](https://arcanum.yandex-team.ru/projects/noapache-video/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2FVIDEO&id=fast-data-release).
2. Ищем Finished релиз на который хотим откатиться и жмём **Rollback to**. Галочки **Cancel other releases** и **Stop autorun** лучше не снимать (только если Вы понимаете что делаете и готовы позже вернуть всё в работающее состояние). Жмём **Run**.
3. Запускается rollback-релиз на стейдже **Deploy**, в нём кубик с таской **DEPLOY_FAST_DATA**, откатывающей фаст-дату на версию из билд таски откатываемого релиза. Смотрим на графики (описание ниже).
4. **!!!ВАЖНО!!!** Когда всё будет готово для возобновления релизов, не забудьте включить **Autorun** тумблером сверху справа на странице CI-проекта из первого пункта.

## Мониторинги {#monitorings}
### Графики {#graphs}
* Графики **процента выкладки web** на которых видно какая версия была активирована в последний деплой: [активация](https://nda.ya.ru/3Vp5Qc), [активация + prepare](https://nda.ya.ru/3Vp5Qy)
* Графики **процента выкладки video** на которых видно какая версия была активирована в последний деплой: [активация](https://nda.ya.ru/t/tFekxkeh5DJPbw), [активация + prepare](https://nda.ya.ru/t/Tqb5Qlqr5DJRax)

### Панели {#panels}
* **WEB** [https://yasm.yandex-team.ru/panel/fast-data](https://yasm.yandex-team.ru/panel/fast-data)
* **VIDEO** [https://yasm.yandex-team.ru/panel/fast-data-video](https://yasm.yandex-team.ru/panel/fast-data-video)

Метрики:
* **noapache-fast-data-version**: текущая версия данных. Может запаздывать с обновлением, так как может быть медленный под, лучше всего оценивать текущую версию по графикам **процента выкладки**.
* **noapache-fast-data-version-diff**: во время переключения должен быть ненулевой, после переключения нулевой.
* **unistat-load_fast_data_success_dmmm**: во время переключения должно пойти вверх.
* **unistat-load_fast_data_error_dmmm**: должно быть в нуле всегда.

## Способ отката, использовавшийся до CI-rollback (в крайнем случае может быть использован) {#deprecated-rollback}
1. Останавливаем релизы в CI (Autorun on -> Off) и прожимаем cancel всем активным релизам: [Fast Data release to WEB](https://a.yandex-team.ru/projects/upper/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast&id=fast-data-web-release), [Fast Data release to VIDEO](https://arcanum.yandex-team.ru/projects/noapache-video/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2FVIDEO&id=fast-data-release).
2. Идем в nanny-сервис: [noapache_fast_data_deployer_web для WEB](https://nanny.yandex-team.ru/ui/#/services/catalog/noapache_fast_data_deployer_web/), [noapache_fast_data_deployer_video для VIDEO](https://nanny.yandex-team.ru/ui/#/services/catalog/noapache_fast_data_deployer_video/).
3. Активируем нужный снепшот (версию фаст-даты можно посмотреть, зайдя в билд таску нужного релиза).
4. Смотрим на графики (описание выше). Через 10-15 минут запустится откат.

### Если нужно откатить ноапачи на стабильные данные, но автоматика не работает {#where-is-my-automatic}
```bash
sky portorun -v -p \
'ln -sfn rfast_stable rfast && \
 PORT=$(jq .properties.BSCONFIG_IPORT -r dump.json) && \
 curl -o /dev/null "localhost:$PORT/admin?action=reload_fast_data&id=yandsearch"' \
f@hamster_noapache_sas_web f@hamster_noapache_man_web f@hamster_noapache_vla_web \
f@production_noapache_sas_web_rkub f@production_noapache_man_web_rkub f@production_noapache_vla_web_rkub
```
