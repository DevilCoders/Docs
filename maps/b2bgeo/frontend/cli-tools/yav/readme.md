# Fetch vault from yav
## How config
1) create in project folder `.yav-meta.json`
```js
[
  {
    // vault name in .env file
    "name": "SOME_LOCAL_VAULT", 
    "source": {
      // source secret uid
      "uid": "sec-xxxxxxxxxxxxxxxxxxxxxxxxxx",
      // source secret name
      "name": "client_secret"
    }
  }
]
```

2) add in project package.json `devDependencies` `"@b2bgeo/yav": "*"`
3) add script in scripts
`"get-secrets": "fetch-secrets"`
4) run script
```sh
npm run get-secrets
```
