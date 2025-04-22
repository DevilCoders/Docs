# Pro Marketplace MVP

|             | Testing                  | Production                     |
| ----------- | ------------------------ | ------------------------------ |
| Marketplace | [Testing][testing]       | [Production][production]       |
| Admin       | [Testing][admin_testing] | [Production][admin_production] |

[testing]: https://taximeter-core.tst.mobile.yandex.net/pro-marketplace
[production]: https://taximeter.yandex.rostaxi.org/pro-marketplace
[admin_testing]: https://tariff-editor.taxi.tst.yandex-team.ru/newsletters/marketplace
[admin_production]: https://tariff-editor.taxi.yandex-team.ru/newsletters/marketplace
[drawio_vscode_extension]: https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio

## Development

```
git clone git@github.yandex-team.ru:taxi/superweb.git
cd superweb/@apps/pro-marketplace/
yarn
yarn vite
```

Open <http://localhost:3000>

## App Business Logic

### Offer Logic

[Open to get drawio editor][drawio_vscode_extension] to edit or read `./scheme.drawio`

### Authentication

Request credential cookies from the backend developer responsible for the service, and set them using developer tools

```
Browser -> Developer tools -> Application -> Storage -> Cookies -> http://localhost:3000
```

| Cookie Name            | Example Value (Example)            |
| ---------------------- | ---------------------------------- |
| `webviewuseragent`     | `Taximeter%209.28%20(1234)`        |
| `webviewparkid`        | `7ad36bc7560449998acbe2c57a75c293` |
| `webviewdriversession` | `aadba2df9ef7409691d9190ef84f2e09` |

### Session (cookies)

1. Install Android Studio from Self Service
2. Make sure to have PATHes in `.zshrc` or `.bash_profile`

```
export ANDROID_SDK_ROOT="/Users/<USERNAME>/Library/Android/sdk"
export PATH="$ANDROID_SDK_ROOT/platform-tools:$PATH"
```

3. Configure Android emulator, start it from `AVD manager`, run sync in empty Android project to download gradle (VPN could block download, disable it)
4. On Android start go to `Settings` -> `About device` -> tap 5 times on `Build number`
5. Get android taximeter app from [dev builder][android_taximeter_app], select one of success builds and navigate to `Artifacts` -> `apk/yandex/apk/development/release/`, download `.apk` file
6. Install it by drag and drop on Emulator, sometimes you have to rename file in order to remove special chars like `taximeter.apk`
7. To create a driver go to [Admin][taximeter_admin] and select `Sea bream` -> on left Menu `Диспа 2.0` -> `Human icon` -> `Drivers` -> `+` or `Add` Button -> fill required fields, also create a new car if needed. Remember driver phone! For testing it shold look like this `+7 000 XXX XX XX` (replace `X` with unique random numbers). Dont forget to add balance for testing purposes, if needed.
8. Auth with phone number in taximeter app
9. To reach pro-marketplase's webview tap on user and find blue card
10. open terminal and run `adb logcat`
11. Open [browser device inspector][webview_dev] and find your device's webview and `inspect` it, go to `Developer tools` -> `Application` -> `Storage` -> `Cookies` and copy values of fields: `webviewuseragent`, `webviewparkid`, `webviewdriversession`
12. Insert values in browser in orer to develop/debug app with React tools. To fasten this process use script below, paste it to console.

```
document.cookie = "webviewuseragent=Taximeter%209.89%20(1073996230); path=/; expires=Tue, 19 Jan 2038 03:14:07 GMT"
document.cookie = "webviewparkid=7ad36bc7560449998acbe2c57a75c293; path=/; expires=Tue, 19 Jan 2038 03:14:07 GMT"
document.cookie = "webviewdriversession=be8671c91e7c43789fc853a5beb7475d; path=/; expires=Tue, 19 Jan 2038 03:14:07 GMT"
```

[taximeter_admin]: https://taximeter-admin.taxi.tst.yandex-team.ru/
[webview_dev]: browser://inspect/#devices
[android_taximeter_app]: https://teamcity.taxi.yandex-team.ru/project/TaximeterAndroidClient?mode=builds

## Deploy

### Testing

Deploy will start automatically after PR gets merged into the `main` branch

Open <https://taximeter-core.tst.mobile.yandex.net/pro-marketplace/>

### Production

Bump `pro-marketplace` version, create PR to the `main` branch, and get it merged

```
cd superweb/@apps/pro-marketplace/
npm version patch
```

Open <https://taximeter.yandex.rostaxi.org/pro-marketplace>
