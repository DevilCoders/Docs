[![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Ir_UltraController/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Ir_UltraController)

Сборка и выкладка компонента `ultra-controller` осуществляется через CD-pipeline https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/ultra-controller-stages


После переезда в аркадию src/main/tmpl будет сама приезжать в нужную директорию и нужно будет выкосить костылики из няни.
Files->"ultra-controller.solomon.tmpl.static" нужно удалить и в InstanceSpec убрать кусок который копирует этот файл из prepare секции.
```bash -c "mkdir -p {BSCONFIG_IDIR}/tmpl/conf/solomon-agent/service.d/; cp -f ultra-controller.solomon.tmpl.static {BSCONFIG_IDIR}/tmpl/conf/solomon-agent/service.d/micrometer-prometheus.conf"``` вот эту штуку нужно будет убрать.