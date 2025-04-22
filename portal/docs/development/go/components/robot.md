# Библиотека robot
Реализация в [a.yandex-team.ru/portal/avocado/libs/utils/robot](https://a.yandex-team.ru/arcadia/portal/avocado/libs/utils/robot)
Модель в [a.yandex-team.ru/portal/avocado/libs/utils/base/models](https://a.yandex-team.ru/arcadia/portal/avocado/libs/utils/base/models/robot.go)
Модель предоставляется base контекстом посредством метода `GetRobot() *models.Robot`.

## Модель
[a.yandex-team.ru/portal/avocado/libs/utils/base/models](https://a.yandex-team.ru/arcadia/portal/avocado/libs/utils/base/models/robot.go)

```go
type Robot struct {
    IsRobot bool
}
```
Поле `Robot.IsRobot` содержит информацию о том, это запрос от робота или нет.

Включает в себя все проверки из перла на роботность:
* Проверяет по header-у `X-Antirobot-Robotness-Y` и `X-Moz`
* Проверяет по uatraits(поле `isRobot`)
* Проверяет по заранее заполенному массиву значений, который храниться в
[a.yandex-team.ru/portal/avocado/libs/utils/robot/useragent.go](https://a.yandex-team.ru/arcadia/portal/avocado/libs/utils/robot/useragent.go).
