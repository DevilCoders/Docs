### Клиент к feature-flag-api

#### Примеры использования

```go
featureFlagClient := featureflag.NewClient(host, serviceCode, logger, httpClient)
flags, err := featureFlagClient.CreateFlags()
flags.IsFlagEnabled("flag")
```

##### С учетом AB
Для флагов, которые можно переопределить через AB,
есть два способа:

1. Предпочтительно использовать этот способ.
   Нужно сложить активные AB флаги в контекст,
   например, в интерцепторе, и передавать контекст для получения значения флага:

```go
ctx = featureflag.WithABFlags(ctx, "flag1", "flag2")

flags.IsFlagEnabledWithAB(ctx, "flag2")
```

2. [Deprecated] Можно передавать `featureflag.ABFlags`,
   чтобы переопределить значение флага значением из AB:

```go
abFlags := featureflag.NewABFlags(map[string]string{
    "flag1": "1",
    "flag2": "0",
    "flag3": "0",
})

flags.IsFlagEnabledABOverride("flag2", abFlags)
```

#### Storage
Хранит в себе `featureflag.Flags`, который обновляется в фоне с интервалом `flagsUpdateInterval`

```go
storage, err := featureflag.NewStorage(&featureFlagClient, updateInterval, logger, clockwork.NewRealClock())
storage.GetFlags().IsFlagEnabled("flag")
```
