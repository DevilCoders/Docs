# Disclaimer

Адаптация [logrus](.com/YandexClassifieds/go-common/log/logrus) к
нашему [формату](https://wiki.yandex-team.ru/vertis-admin/logs/logsformat/?from=%252Fvertis-admin%252Flogs_format%252F).

Подробнее: https://wiki.yandex-team.ru/vertis-admin/logs/

## Example

```go
package main

import (
	"github.com/YandexClassifieds/go-common/log/logrus"
	"github.com/getsentry/sentry-go"
)

func main() {
	err := sentry.Init(sentry.ClientOptions{
		Dsn: "my-sentry-dsn",
	})
	log := logrus.New(logrus.WithLevel("debug"), logrus.WithSentry())
	if err != nil {
		log.WithError(err).Fatal("failed to init sentry")
    }
	log.Debug("this a debug message")
}
```