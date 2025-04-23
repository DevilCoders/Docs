# Установка ansible
### MacOS
Необходимые пререквизиты для установки:
1. Установленный Homebrew
    ```
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```
1. Установленный xcode
    ```
    xcode-select --install
    ```
2. Установленный python3
    ```
    brew install python3
    ```

После выполненных пререквизитов ставим ansible
```
brew install ansible
```

### MacOS и возможные проблемы с python:
1. Проблема: `ERROR:root:code for hash md5 was not found - not able to use any hg mercurial commands`

    **Решение:**
     ```
    brew upgrade openssl
    ```   
     ```
    ls /usr/local/Cellar/openssl
    ```
    ```
    brew switch openssl {версия из команды выше}
    ```
    ```
    python -c "import hashlib;m=hashlib.md5();print(m.hexdigest())"
    ```
   [Источник](https://stackoverflow.com/questions/59269208/errorrootcode-for-hash-md5-was-not-found-not-able-to-use-any-hg-mercurial-co)
2. Проблема: `Error: No available formula with the name "python@2"`

   **Решение:**
   ```
    brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/86a44a0a552c673a05f11018459c9f5faae3becc/Formula/python@2.rb
   ```
   [Источник](https://stackoverflow.com/questions/60298514/brew-reinstalling-python2/60345962#60345962)
3. Проблема: `Invalid dylib load. Clients should not load the unversioned libcrypto dylib as it does not have a stable ABI.`

   **Решение:**
   ```
   brew install openssl
   ```
   ```
   export DYLD_LIBRARY_PATH=/usr/local/opt/openssl/lib:$DYLD_LIBRARY_PATH
   ```
   [Источник](https://stackoverflow.com/a/58445755)

Так же есть специальная страничка, куда складываем решения возникающих проблем:
https://wiki.yandex-team.ru/users/caulfield/newcomers-devux/
