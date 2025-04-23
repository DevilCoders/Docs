maps_core_masstransit.jinja - common yasm panel template for masstransit services.
Current active version is stored in yasm at https://yasm.yandex-team.ru/template/panel/maps_core_masstransit and edited via UI. But UI does not provide versions history, so we store it in SVN here.

Set template parameters (itype=maps, ctype=<staging>, and prj=<project>) to get the panel.
For example, mtinfo testing panel: https://yasm.yandex-team.ru/template/panel/maps_core_masstransit/itype=maps;ctype=testing;prj=maps-core-masstransit-mtinfo/

More info about the meaning of the parameters:
  * https://wiki.yandex-team.ru/maps/dev/core/Instrukcija-po-sozdaniju-servisov-v-RTC/newserviceinrtc/gencfg/#sozdaemgruppu
  * https://wiki.yandex-team.ru/maps/dev/core/Instrukcija-po-sozdaniju-servisov-v-RTC/naming/#imenaservisovvrtc

The template generates panel on the fly, so it updates the list of hosts and yacare handles automatically, but the panel generation could be a bit slow.
Also you could save the generated panel as a separate panel - it will be shown much faster, but you lose the autoupdates of the hosts and handles.
