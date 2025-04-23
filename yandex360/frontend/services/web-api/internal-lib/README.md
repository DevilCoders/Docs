[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/web-api/internal-lib&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/web-api/internal-lib)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/web-api/internal-lib&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/web-api/internal-lib)

# Библиотека общего серверного кода интерфейсов Яндекс.Почты

Поставляется как npm-пакет `@ps-int/mail-lib`

## Содержит

- `Модели`
- `Сервисы`
- `Конфиги сервисов`
- `Доменные конфиги`
- `Миддлвары`
- `Вспомогательные хелперы`
- библиотеку `moe` для «деклатаривного» описания сервисов и методов.

## Локализация
Не текущий момент в локализации есть переводы для папок, меток и фильтров фуриты.
Обновляется командой
```bash
npm run i18n-update
```
Ключи берутся из проекта [Mail API](https://tanker.yandex-team.ru/?project=mail-api&branch=master).

[**Интерфейс модуля**](https://github.yandex-team.ru/personal-services/frontend/blob/dev/services/web-api/internal-lib/index.js)

[**Интерфейс библиотеки moe**](https://github.yandex-team.ru/personal-services/frontend/blob/dev/services/web-api/internal-lib/moe.js)

Оба интерфейса должны слиться в один.
