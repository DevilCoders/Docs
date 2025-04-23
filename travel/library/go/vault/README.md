# Vault library
Библиотека для работы с секретницей.
## Usage
Конструктор NewYavSecretsResolver берет токен из переменной TRAVEL_VAULT_OAUTH_TOKEN. NewYavSecretsResolverFromEnv позволяет передать имя переменной для получения токена. Пример: 
```
r := vault.NewYavSecretsResolverFromEnv(<token envName>)
```
Для получения секрета надо указать secret_uuid или version и key
```
secValue, err := r.GetSecretValue(<secret_uuid/version>, <key>)
```

