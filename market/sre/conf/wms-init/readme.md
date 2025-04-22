# Набор systemd юнитов для запуска сервисов WMS

По-умолчанию не добавляются в автозапуск. Требует явный рагумент - номер ноды.  
Порядок запуска и лимиты взяты из тикета https://st.yandex-team.ru/MARKETWMS-1383  

**@1 - номер ноды**

### First install:
1. Раскатываем пакет через [ЦУМ](https://tsum.yandex-team.ru/pipe/projects/wms/delivery-dashboard/wms-init)
2. Заходим в `/opt/infor/sce/scprd/bin/sce_menu.sh`
3. Делаем Shutdown All(2)
4. `systemctl enable scprd-excelplugin@1 && systemctl enable scprd-reports@1 && systemctl enable scprd-scheduler@1 && systemctl enable scprd-uiservice@1 && systemctl enable scprd-wmbatch@1 && systemctl enable scprd-wmoltp@1 && systemctl enable scprd-wmsocket@1`
5. Проверяем запуск oltp: `systemctl start scprd-wmoltp@1`
6. `systemctl status scprd-wmoltp@1`
7. Запускаем все systemctl start scprd-wmoltp@1 && systemctl start scprd-wmbatch@1 && systemctl start scprd-excelplugin@1 && systemctl start scprd-uiservice@1 && systemctl start scprd-wmsocket@1 && systemctl start scprd-scheduler@1 && systemctl start scprd-reports@1
-------------

#### FULL STOP:
```
systemctl stop scprd-wmoltp@1 scprd-wmbatch@1 scprd-excelplugin@1 scprd-uiservice@1 scprd-wmsocket@1 scprd-scheduler@1 scprd-reports@1
```

#### FULL RESTART:
```
systemctl restart scprd-wmoltp@1 scprd-wmbatch@1 scprd-excelplugin@1 scprd-uiservice@1 scprd-wmsocket@1 scprd-scheduler@1 scprd-reports@1
```

#### FULL START
```
systemctl start scprd-wmoltp@1 scprd-wmbatch@1 scprd-excelplugin@1 scprd-uiservice@1 scprd-wmsocket@1 scprd-scheduler@1 scprd-reports@1
```

-------------
Пример включения для первой ноды:  
```
systemctl enable scprd-excelplugin@1
systemctl enable scprd-reports@1
systemctl enable scprd-scheduler@1
systemctl enable scprd-uiservice@1
systemctl enable scprd-wmbatch@1
systemctl enable scprd-wmoltp@1
systemctl enable scprd-wmsocket@1
```

Для запуска всех сервисов последовательно:  
```
systemctl start scprd-wmoltp@1
systemctl start scprd-wmbatch@1
systemctl start scprd-scheduler@1
systemctl start scprd-reports@1
systemctl start scprd-uiservice@1
systemctl start scprd-excelplugin@1
systemctl start scprd-wmsocket@1
```