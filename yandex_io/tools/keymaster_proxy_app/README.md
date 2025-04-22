# Keymaster test app

## How to build & deploy

```
ya make --target-platform DEFAULT-ANDROID-ARMV8A -DYANDEXSTATION -DARCAIDA_CURL_DNS_RESOLVER=MULTITHREADED && adb push keymaster_proxy_app /data && adb shell chmod +x /data/keymaster_proxy_app
```

## How to use

```
adb shell /data/keymaster_proxy_app sign /data/inputs/1mb /data/signs/1mb.sign
```
