# General Themes
![npm stable version](https://badger.yandex-team.ru/npm/@ps-int/general-themes/version.svg)

Коллекция конфигов и ресурсов для общих кросссервисных тем.

## Разработка

### Сборка и публикация

```bash
# в директории пакета
# версия по semver
npm run package -- X.Y.Z
```

## Использование

Пакет состоит из нескольких частей:
- информация про статические файлы для тем, в виде, совместимом с `@ps-int/cover-layer`;
- абстракция для работы с настройкой общих тем в Датасинке `GeneralThemesSettingsDatasyncService`.
- логика для работы с промо: `GeneralThemesPromoLogic` и `GeneralThemesPromoDatasyncApi`

Со стороны сервиса необходим `@ps-int/datasync-client`

## FAQ

Документация ко всем методам и их параметры доступны через JSDoc.

### Как включить/отключить тему 360?
> Вместе с включением темы можно включить анимацию фонов, см. документацию к методу
```
GeneralThemesSettingsDatasyncService#enableTheme()
GeneralThemesSettingsDatasyncService#disableTheme()
```

### Как включить/отключить анимацию видео-фонов тем 360?
```
GeneralThemesSettingsDatasyncService#enableVideoBg()
GeneralThemesSettingsDatasyncService#disableVideoBg()
```

### Как понять, надо ли показывать промо тем 360?
```
GeneralThemesPromoLogic#shouldShowFullscreen
GeneralThemesPromoLogic#shouldShowTooltip
```

### Как отметить, что промо были показаны?
```
GeneralThemesPromoDatasyncService#setFullscreenShownDate()
GeneralThemesPromoDatasyncService#setTooltipShownDate()
```

## Статика тем

TBD
