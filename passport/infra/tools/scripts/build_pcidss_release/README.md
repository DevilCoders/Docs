Один раз надо подготовить окружение:
```
 ./prepare_env.sh
```

Собрать релиз:
1. имя бранча
2. путь к пакету
3. список репозиториев на заливку через `;`
4. идентификатор GPG-ключа для подписи пакета

Например:
```
 ./build_release.sh \
    releases/passport/yandex-passport-tvmknife-6 \
    passport/infra/tools/tvmknife/debianization/debian.json \
    "passport" \
    3DF9F77838AC96FE
```
