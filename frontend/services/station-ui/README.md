# Интерфейс Яндекс.Станции

Тут нет:

- Полноценного скелета "боевого" приложения, нет redux, нет примеров работы с bem-react:v3 и тд
- Нет никакого логирования скорости/ошибок приложения, за исключением того что логирует сам апхост/rr
- Нет метрик: либо Я.Метрики, либо баобаба
- Конфиги гермионы/вебпака и т.д. предоставляют самую базу, в реальных проектах они немного/много сложнее
- Не подключены заголовки CSP

## Storybook

Начало работы

```(bush)
npm run storybook:build

npm run storybook
```

Чтобы добавить компонент, необходимо создать файл  `<имя компонента>.stories.tsx` в директории  `src/components`.

# Полезная информация

- Различные хелпер-команды по работе с апхостом, можно посмотреть запустив `npx archon --help` после создания сервиса
- Про apphost можно почитать здесь https://doc.yandex-team.ru/apphost/ и здесь https://wiki.yandex-team.ru/search-interfaces/infra/dev-at-apphost
- TS Пакет с тайпингами и API для работы с контекстом апхоста: https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/frontend-apphost-context
- Про Archon https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon
- Про Kotik https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/kotik
