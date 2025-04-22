
## Scripts for running autotests on the emulator and real devices
WiKi: https://wiki.yandex-team.ru/tv-android/testing/androidtvautomation/

#### Dependencies:
* SDK/cmdline-tools (SDK/tools is is deprecated)
* Java 11
* Python 3.7+
* requests==2.27.1 - ```python3 -m pip install requests==2.27.1```
* retrying==1.3.3 - ```python3 -m pip install retrying==1.3.3```
* avdmanager for run emulator
* apksigner for sign apps
* yandex-passport-vault-client - ```sudo apt-get install -y yandex-passport-vault-client```
* access to secret [android-tv-autotests](https://yav.yandex-team.ru/secret/sec-01fsrr8cgn5tq5bref1fecnx43)

.bashrc example:
```console
export ANDROID_SDK_ROOT=$HOME/Android/sdk
export ANDROID_HOME=$HOME/Android/sdk
export PATH=${PATH}:$ANDROID_HOME/platform-tools
export PATH=${PATH}:$ANDROID_HOME/emulator
export PATH=${PATH}:$ANDROID_HOME/cmdline-tools/latest/bin
export PATH=${PATH}:$ANDROID_HOME/build-tools/29.0.2
```

#### Install packages for emulator
* for tv:
```console
command: yes | sdkmanager "system-images;android-25;android-tv;x86"
```
* for station:
```console
command: yes | sdkmanager "system-images;android-28;google_apis;x86_64"
```
* for centaur:
```console
command: yes | sdkmanager "system-images;android-28;google_apis;x86"
```

#### Run script

```console
python3 tv/ci/ui-tests/run_tests.py --help
```

##### Options

###### env
* `--branch`
    * default value is trunk
* `--signer_token`
    * by default, token is used from `/.yandex/yandex-signer.properties` [WiKi](https://wiki.yandex-team.ru/yandexmobile/techdocs/mobbuild/yandex-signer/#kakukazattoken)
* `--testpalm_token`
    * token for send report to testpalm [WiKi](https://wiki.yandex-team.ru/testpalm/testpalmdoc/api/)
* `--tus_token`
    * token for get account [WiKi](https://wiki.yandex-team.ru/test-user-service/)

###### for tests
* `--product`
  * default value is `tv`
  * values: `tv`, `station`, `centaur`, `tv-updater`, `tv-services`
* `--droideka_url`
    * default value is `https://droideka.smarttv.yandex.net`
* `--ya_login`
    * login for yandex account in tests
    * default value will be taken from [TUS](https://wiki.yandex-team.ru/tv-android/testing/androidtvautomation/#akkauntydljaavtotestovitokeny)
* `--ya_pass`
    * password for yandex account in tests
    * default value will be taken from [TUS](https://wiki.yandex-team.ru/tv-android/testing/androidtvautomation/#akkauntydljaavtotestovitokeny)
* `--test_suite`
    * default value is `Acceptance`
    * values: `Acceptance`, `Regression`, `DroidekaRegression`, `ModuleRegression`, `UpdaterAcceptance`, `ServicesSdkTests`, `UpdaterIsolatedAcceptanceTests`
* `--test_class`
    * for run all tests in class > provide class name. Example: `SearchScreen`
    * for run only one test > provide test name. Example: `SearchScreen#checkAllElements`
* `--testpalm_report`
    * send report to testpalm
    * default value is `false`

###### emulator
* `--emulator_api`
    * android API for start emulator. `25` for use android 7.1.1 `28` for use android 9.0
    * default value is `25`
* `--emulator_resolution`
    * emulator resolution. `1080` for use 1920x1080 and `720` for use 1280x720
    * default value is `720`

###### real device
* `--serial_number`
    * Device IP or ID of module

###### for debugging
* `--emulator_only`
    * `true` for run only emulator with yandex apps
    * default value is `false`
* `--delete_emulator`
    * `true` for stop and delete emulator after tests
    * default value is `false`
* `--skip_build_services`
    * `true` for skip this step
* `--skip_build_updater`
    * `true` for skip this step
* `--skip_build_video_player`
    * `true` for skip this step
* `--skip_download_apps`
    * `true` for skip this step
* `--is_sign_apps`
    * `false` for skip this step
    * default value is `true`
* `--quasar_id`
    * You can set your own quasar ID. You need to create a config [here](https://quasmodrom-test.quasar-int.yandex-team.ru/admin/development/device/)
    * or use config with droideka prod - `2a269aaa98724c64dca4-emulator-prod`
    * default value is `2a269aaa98724c64dca4-emulator` [quasmodrom](https://quasmodrom-test.quasar-int.yandex-team.ru/admin/development/device/details/?id=466930&url=%2Fadmin%2Fdevelopment%2Fdevice%2F)

##### Examples

###### Run yandex TV emulator
```console
python3 tv/ci/ui-tests/run_tests.py --product="tv" --emulator_only="true"
```

```console
python3 tv/ci/ui-tests/run_tests.py \
--product="tv" \
--emulator_only="true" \
--skip_download_apps="true" \   # if the apps are already downloaded
--emulator_api=25 \             # `25` for use android 7.1.1 `28` for use android 9.0
--quasar_id="id_name"           # your custom config
```

###### Run Station emulator
```console
python3 tv/ci/ui-tests/run_tests.py --product="station" --emulator_only="true"
```

###### Run Centaur emulator
```console
python3 tv/ci/ui-tests/run_tests.py --product="centaur" --emulator_only="true"
```

###### Start Acceptance tests on TV emulator (first launch)
```console
python3 tv/ci/ui-tests/run_tests.py --test_suite=Acceptance   # (UpdaterAcceptance, ServicesSdkTests)
```

###### Start Acceptance tests on TV emulator
```console
python3 tv/ci/ui-tests/run_tests.py \
--skip_build_updater="true" \
--skip_build_services="true" \
--skip_build_video_player="true" \
--skip_download_apps="true" \
--test_suite="Acceptance"
```

###### Start one test on TV emulator
```console
python tv/ci/ui-tests/run_tests.py \
--skip_build_updater="true" \
--skip_build_services="true" \
--skip_build_video_player="true" \
--skip_download_apps="true" \
--test_suite="Regression" \
--test_class="SearchScreen#checkAllElements"
```

###### Start one test on Station emulator
```console
python tv/ci/ui-tests/run_tests.py \
--product="station" \
--test_class="AliceIntegration#testSimpleQuestion"
```

###### Start Acceptance tests on real TV or Module
```console
python3 tv/ci/ui-tests/run_tests.py \
--serial_number="192.168.1.124" \       # for module use --serial_number="D00Z20000FT6GW"
--test_suite=Acceptance
```

###### Start one test on real TV or Module
```console
python3 tv/ci/ui-tests/run_tests.py \
--serial_number="192.168.1.124" \
--test_class="SearchScreen#checkAllElements"
```

###### Start one test on real Station
```console
python3 tv/ci/ui-tests/run_tests.py \
--serial_number="192.168.1.113" \
--product="station" \
--test_class="AliceIntegration#testSimpleQuestion"
```

###### Start Regression tests in kolhoz (TV, Module)
```console
python3 tv/ci/ui-tests/run_tests.py \
--product="tv" \
--kolhoz_token="AQAD-qJSK......" \
--kolhoz_device_id="9cf14ffb-dab8-467b-ad83-fb3b1cf39217" \
--test_suite="Regression"
```

###### Start one test in kolhoz (Station)
```console
python3 tv/ci/ui-tests/run_tests.py \
--product="station" \
--kolhoz_token="AQAD-qJSK......" \
--kolhoz_device_id="9cf14ffb-dab8-467b-ad83-fb3b1cf39217" \
--test_class="SearchScreen#checkAllElements"
```

###### Start Acceptance tests on Centaur emulator
```console
python3 -u tv/ci/ui-tests/run_tests.py \
--product=centaur \
--test_suite=Acceptance \
--is_sign_apps=false
```

###### Start one test on Centaur emulator
```console
python3 -u tv/ci/ui-tests/run_tests.py \
--product=centaur \
--is_sign_apps=false
--test_class="MainScreen#checkDeviceInitialization"
```

###### Start Services IPC Tests (TV)
```console
python3 -u tv/ci/ui-tests/run_tests.py \
--product=tv-services \
--test_suite=ServicesSdkTests \
--is_sign_apps=false
```

###### Start Updater Isolated Acceptance Tests (TV)
```console
python3 -u tv/ci/ui-tests/run_tests.py \
--product=tv-updater \
--test_suite=UpdaterIsolatedAcceptanceTests \
--is_sign_apps=false
```

###### Update OTA on device

1. Download OTA file:

- [hikeen_rt2871](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=yandex_android_tv_Realtek2871_Rt2871sandboxDemo&tab=buildTypeStatusDiv)
  file - 240_RealtekATV_40in_RealtekATV_rt2871_{BRANCH}_userdebug_{OTA_BUILD_NUMBER}-OTA.zip
- [cvte_hisi351](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=android_tv_SandboxRomCvte351userdebug&tab=buildTypeStatusDiv)
  file - YANDEX_DEBUG_TV24_H24F8000Q_CP666777_cvte351_{BRANCH}_userdebug_{OTA_BUILD_NUMBER}-OTA.zip
- [cvte_mt6681](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=android_tv_Hisilicon351_SandboxRomCvte6681userdebug)
  file - YANDEX_TV32_SK506S_PB802_PT320AT02_2_CS548913_cvte6681_{BRANCH}_userdebug_{OTA_BUILD_NUMBER}-OTA.zip
- [cv_mt9632](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=yandex_android_tv_Cultraview9632_SandboxRomCultraview9632userdebug&tab=buildTypeStatusDiv)
  file - YANDEX_DEBUG_TV50_WIFI-RTK88X2CU_cv9632_{BRANCH}_userdebug_{OTA_BUILD_NUMBER}-OTA.zip
- [cv_mt6681](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=android_tv_Cultraview6681_SandboxRomCultraview6681userdebug)
  file - YTV_YH32CV6681.T320XVN02G_KVANT-T320XVN02G_cv6681_{BRANCH}_userdebug_{OTA_BUILD_NUMBER}-OTA.zip

2. Put OTA file in a folder `arc/arcadia/smart_devices/android`

3. Run command:
```console
python3 tv/ci/ui-tests/ota_update.py --serial_number="192.168.1.124" --ota_build_number=1947
```

### links
- WiKi: https://wiki.yandex-team.ru/users/doroninaya/YANDEX-ECOSYSTEM-TESTING/androidTvAutomation/
- teamcity: https://teamcity.yandex-team.ru/project.html?projectId=YandexTvHome_Tests
