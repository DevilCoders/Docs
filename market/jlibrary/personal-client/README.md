### Описание

Клиент для Personal. Использует авторизацию TVM

### Как использовать
1. Подключить библиотеку к себе в проект. В `ya.make` в секцию `PEERDIR` добавить `market/jlibrary/personal-client`
2. Убедиться что есть бин ```TvmClient``` в спринговом контексте 
3. Импортировать спринговый конфиг ```@Import(PersonalClientConfiguration.java.class)```
4. Добавить необходимые проперти:
```
personal.url
personal.tvmServiceId
personal.connectTimeoutMillis --по умолчанию 20_000
personal.readTimeoutMillis --по умолчанию 10_000
personal.maxConnTotal --по умолчанию 10
```

