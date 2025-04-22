## Глобальные флаги 
Глобальные флаги живут в Бункере
- Android - https://bunker.yandex-team.ru/mailfront/mmapi-flags/android?view=raw
- iOS     - https://bunker.yandex-team.ru/mailfront/mmapi-flags/ios?view=raw

И описываются конфигом на TypeScript
- Android - `android.ts`
- iOS - `ios.ts`

### Как обновить
1) Надо внести изменения в `android.ts`/`ios.ts`
2) Сделать пул-реквест в мастер
3) После мержа пул ревеста флаги автоматически загрузятся в бункер таской в Тимсити
https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_Mail_Common_MailCommonXMailFlagsUpdate
4) После выполнения таски надо пойти в бункер по ссылкам выше и нажать на кнопку "Опубликовать" 
5) Через 5 минут новые флаги появятся в проде
- Android - https://mail.yandex.ru/api/mobile/v2/flags?uuid=1&client=aphone
- iOS     - https://mail.yandex.ru/api/mobile/v2/flags?uuid=1&client=iphone
