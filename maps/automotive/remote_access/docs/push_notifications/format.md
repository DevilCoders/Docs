### Формат уведомлений

```json
{
    "type": "EngineStart", // строковый идентификатор
    "title": "Заголовок нотификации",
    "appName": "autoapp",
    "description": "Запуск двигателя",
    "severity": "Info", // "Info", "Warning" или "Danger"
    "datetime": "2019-07-26T12:18:56.197+0000",
    "carName": "RAV4",
    "plateNumber": "X000AA000", // регистрационный номер
    "carId": "0000-1111..." // Id автомобиля
}
```

** Поля title и description на android будут показаны в UI (как заголовок и текст уведомления) **

### Список уведомлений

*    Тревога: машина в движении // type="AlarmMovement"
*    Двигатель заведён // type="EngineStart"
*    Двигатель заглушён // type="EngineStop"
*    Машина закрыта // type="Lock"
*    Машина открыта // type="Unlock"
*    Тревога выключена // type="Unlock"
*    Не удалось закрыть машину, проверьте двери и багажник // type="CannotLock"
*    Не удалось закрыть машину, проверьте капот// type="CannotLock"
*    Багажник открыт // type="OpenTrunk"
*    Включен режим обслуживания // type="Maintenance"
*    Низкий заряд аккумулятора // type="BatteryLow"
*    Низкий баланс на сим-карте в машине // type="NoMoney"
*    Осталось 10% топлива // type="EmptyTank"
*    Нет связи с машиной // type="ConnectionLost"
*    Двигатель не заводится // type="CannotStartEngine"
*    Двигатель не заводится. Проверьте положение коробки передач // type="CannotStartEngine"
*    Двигатель не заводится. Проверьте центральный замок // type="CannotStartEngine"
*    Нужно сначала открыть машину и завести двигатель // type="CannotTurnOnServiceMode"
