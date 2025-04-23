# Танкер

> Внимание! Информация в данном разделе неполная. Ознакомьтесь дополнительно с [документацией СЕРПа](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/docs/systems/i18n.md) про переводы.
> В ближайшее время раздел будет актуализирован.

> **Термины**
>
> **Кейсет** – множество ключей, связанных какой-то логикой. В нашем случае это БЭМ-сущность (без уровня), например  b-page__title.
>
> **Ключ** - это фраза или слово.
>
> **Контекст** – контекст, в котором используется ключ.
>
> В коде это выглядит так:
>```javascript
>text = BEM.I18N('название-кейсета', 'ключ', {
>    context: 'описание контекста, в котором используется ключ'
>});
>```
>
>Например:
>```javascript
>text = BEM.I18N('images-touch-viewer2', 'Открыть', {
>    context: 'Кнопка, открывающая картинку на внешнем сайте'
>});
>```

## Получение токена

Танкер использует OAuth-токен для авторизации к своему API. Для генерации персонального токена необходимо:
* Перейти по ссылке https://nda.ya.ru/3SjQY7
* Экспортировать ключ в $HOME/.profile, добавив **export TANKER_API_TOKEN="Тут OAuth токен для Танкера"**
* Не забыть выполнить source $HOME/.profile
* Затем запрашиваем доступ через [IDM](https://idm.yandex-team.ru). "Запросить роль" > "Cистема - Танкер" > "Тип - Проект" > "Images/Video/Multimedia islands" > "Тип - Общие для проекта" > "Разработчик проекта"

## Команды запуска

```bash
fiji tanker # аналог fiji tanker images video sakhalin
fiji tanker images
fiji tanker sakhalin
fiji tanker images/some-block/
```
Если запрос в Танкер падает через определенный тайм-аут, то, возможно, следует установить [сертификат Яндекса](https://wiki.yandex-team.ru/security/ssl/sslclientfix/)

На сервисах Картинки и Видео ключи автоматически отправляются переводчикам по понедельникам и четвергам.
После этого их нужно синхронизировать через команды указанные выше.

## Полезные ссылки
- [СЕРПовая документация](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/docs/systems/i18n.md)
- Больше информации про Танкер - [на Вики](https://wiki.yandex-team.ru/search-interfaces/tanker/tanker-kit/).
- Информация по использованию i18n на TypeScript - [в README проекта i18n](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/i18n#i18n).

