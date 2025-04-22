# Пакет для генерации названий функций

## Зачем?
* фиксируем форматы для ошибок, спанов и т.д.
* меньше копипасты названий - меньше косяков при рефакторинге

## Как?

```go
import (
    "github.com/opentracing/opentracing-go"

    "a.yandex-team.ru/travel/library/go/funcnames"
)

var fnName funcnames.Caller

func init() {
    fnName = funcnames.BuildFullName(getPrivateFnName)
}

func getPrivateFnName() error {
    span, _ := opentracing.StartSpanFromContext(ctx, fnName.String())
    defer span.Finish()

    return fnName.WrapError(xerrors.New("some internal error"))
}

```
