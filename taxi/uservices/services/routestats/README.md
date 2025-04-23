## Wiki

https://wiki.yandex-team.ru/taxi/backend/product/client/routestats-service/

## Help

```bash
make help-routestats
```

### Build with sanitizers

See [the task](https://st.yandex-team.ru/TAXICOMMON-2603) for sanitizers and distcc compatibility.

```bash
ssh distcc-xenial-01.man.yp-c.yandex.net mkdir -p /home/$USER/uservices/userver/cmake/
scp $HOME/uservices/userver/cmake/sanitize.blacklist.txt distcc-xenial-01.man.yp-c.yandex.net:/home/$USER/uservices/userver/cmake/sanitize.blacklist.txt
scp $HOME/uservices/sanitize.blacklist distcc-xenial-01.man.yp-c.yandex.net:/home/$USER/uservices/sanitize.blacklist

ssh distcc-xenial-02.vla.yp-c.yandex.net mkdir -p /home/$USER/uservices/userver/cmake/
scp $HOME/uservices/userver/cmake/sanitize.blacklist.txt distcc-xenial-02.vla.yp-c.yandex.net:/home/$USER/uservices/userver/cmake/sanitize.blacklist.txt
scp $HOME/uservices/sanitize.blacklist distcc-xenial-02.vla.yp-c.yandex.net:/home/$USER/uservices/sanitize.blacklist

make cmake-routestats && make build-with-sanitizers
make build -j16 # to rebuild
```

## Testing

```bash
make testsuite-noenv-routestats RUNTEST_ARGS="-k NEEDED_TEST_NAME"
make utest-routestats
```

## Formatting, checking

```bash
make format-routestats
find schemas/services/protocol-routestats -type f | xargs taxi-eolfmt
find schemas/services/protocol-routestats -name "*.yaml" | xargs taxi-yamlfmt

make check-pep8-routestats
find services/routestats/ -name "*.[ch]pp" | xargs clang-format-9 -i
```

## Static analysis

```bash
./services/routestats/src/tools/gen_clang_tidy_config.py
make clang-tidy-routestats
```

Spell-checking:

```bash
curl -L https://git.io/misspell | bash
sudo mv ./bin/misspell /usr/local/bin/
find ./services/routestats -type f | xargs misspell
```

## Update schemas

```bash
cp -r schemas/services/protocol-routestats ~/schemas/schemas/services/
```
