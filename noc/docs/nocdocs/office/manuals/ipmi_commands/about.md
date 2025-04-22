**Диагностические команды:**    Желательно сборать информацию по датчикам/сенсорам при аварийных ситуациях    1. посмотреть состояние датчиков локально: **`ipmitool sdr`**    2. посмотреть известные датчики с границами: **`ipmitool sensor`**    3. проверить состояние питания локально: **`ipmitool power status`****Активные команды:**    При проблемах с ребутом через консоль/web/kvm, можно отправить сигнал на ребут через ipmi    1. выключить/включить питание удалённо: **`ipmitool -H HOST -U LOGIN -P PASSWORD power off/on`**    Если не помогло, то     отресетить: **`ipmitool -H HOST -U LOGIN -P PASSWORD chassis power reset`**    2. включить питание удалённо: **`ipmitool -H HOST -U LOGIN -P PASSWORD power on`**

    3. если завис BMC: локально **`ipmitool mc reset cold`** удаленно **`ipmitool -H HOST -U LOGIN -P PASSWORD bmc reset cold`**    если не помогло то **`ipmitool mc reset warm`**

При необходимости можно пробросить ssh туннель: **`ssh -L 9999:[ip-ipmi]:443 -N -T noc-myt.yndx.net`** открывать с **`localhost:9999`**    Остальные команды можно посмотреть просто **`ipmitool`** или **`ipmitool help`** или почитать более подробно **`man ipmitool`**

**Сценарии использования**
1. Рыбка и тп. зависла не реагирует на команды:-Собрать диагностику `ipmitool -H HOST.ipmi.yndx.net -U USER -P PASSWORD sdr/sensor`-Отправить в ребут `ipmitool -H HOST -U LOGIN -P PASSWORD chassis power reset`
2. Ipmi не открывается, но до него идут пинги, вероятно подвис-перезагрузить `ipmitool mc reset cold`, если не помогло `ipmitool mc reset warm`, если и так не помогло разбираться в причинах, возможно проблема не в BMC
3. По каким то причинам не открывается web через РТ -пробросить порты и открывать с localhost `ssh -L 9999:[ip-ipmi]:443 -N -T noc-myt.yndx.net`