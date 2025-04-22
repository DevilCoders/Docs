# cmnt-request-regression
Tool for automated integration testing with Payments (sell.yandex.ru)

### Quick start
```bash
# 1. Make binary
$ ya make

# 2. Run all tests
./regression \
  --env <testing/production> \
  --cookie 'yandexuid=*; Session_id=*; sessionid2=*;' \
  --tvm-secret <secret>

# 3. Debug failed tests
./regression \
  --env <testing/production> \
  --cookie 'yandexuid=*; Session_id=*; sessionid2=*;' \
  --tvm-secret <secret> \
  --only <test_name> \
  --debug
```
