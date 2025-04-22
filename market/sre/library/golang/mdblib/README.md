
Библиотека для работы с MDB через GRPC.

Пример использования:
```
if cloudKeyPath.IsExists() {
    //почитать cloud key файл
    cloudKeyFunc = mdblib.ReadCloudKey(cloudKeyPath)
} else {
    //получить OAuth токен
    cloudKeyFunc = mdblib.GetMDBTokenOverSSH(cntx, clientID, clientSecret)
}

//устанавливаем первое соединение для получения аутенфикационного токена
conn, err := mdblib.NewDealer(cntx)
iamfunc := mdblib.GetAIMToken(conn, cloudKeyFunc)
if err != nil {
	logger.Fatalf("%s", err)
}
//токен получен, устанавливаем соединение для работы с MDB
conn, err = mdblib.NewDealer(cntx, mdblib.WithAIMToken(iamfunc))
if err != nil {
	logger.Fatalf("error connect to RPC, %s", err)
}

//дальше можно работать с самим MDB. Например получить список проектов
projects, err := mdblib.ListProjects(conn)
if err != nil {
	logger.Fatalf("error get projects, %s", err)
}
```

Функции:
    mdblib.ListProjects - получить список проектов(покажет все доступные для аккаунта)
    mdblib.ListFolders - получить список папок(покажет все доступные для аккаунта)
    mdblib.ListMongoDatabases - получить список mongo баз
    mdblib.ListMySQLDatabases - получить список mysql баз
    mdblib.ListPostgressDatabases - получить список postgress баз
