###Блок i-device-info:

@see [i-device-info](../../blocks-common/i-device-info/)

##### Поведение `ScreenW` и `ScreenH`
Предполагается, что устройство в landscape ориентации - т. е. screenW > screenH

Если значения `ScreenW` и `ScreenH` *уже* записаны, проверяем, верна ли ориентация(W больше H):
  1. Проверяем, верные ли записаны значения в `ScreenW` и `ScreenH`, и перезаписываем, если значения не верные
  2. Если нет, то меняем местами `ScreenW` и `ScreenH` и выполняем проверку *1*.
