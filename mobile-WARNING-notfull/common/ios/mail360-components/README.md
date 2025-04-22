# Mail360Components pod integration tips

For correct integration add queries schemes in host application `Info.plist`

```xml
<key>LSApplicationQueriesSchemes</key>
<array>
        <string>telemost</string>
        <string>yandexmail</string>
        <string>yandexdisk</string>
</array>
```

## Translations

Use `YXMail360Components/update_translations.sh` to update strings from tanker

## Publishing steps

Pod can be published to [disk-pods-repo](https://bb.yandex-team.ru/projects/MOBDISK/repos/mobile-disk-pods/browse)

1. Update verion in `YXMail360Components.podspec`
2. Run `../../../common/tools/fastbuild/fastlane.sh publish_mail360_pod s3AccessKey:"%ID_ACCESS_KEY%" s3SecretAccessKey:"%SECRET_ACCESS_KEY%"`. Tokens can be obtained using an [instruction](https://wiki.yandex-team.ru/mds/s3-api/authorization/#sozdanieaccesskey). Or you can use token from [robot-keanu-reaves](https://yav.yandex-team.ru/secret/sec-01e0d35mnhd7wp91qxy8htcvgs/explore/versions)
3. Tag published commit:

```bash
arc tag releases/mobile/disk/mail360-components/%VERSIONS%
arc push -u tags/releases/mobile/disk/mail360-components/%VERSIONS%
```
