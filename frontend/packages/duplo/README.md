# Duplo

Общая библиотека блоков рекламных технологий.

- [**Wiki**](https://wiki.yandex-team.ru/duplo/)
- [**ABC Service**](https://abc.yandex-team.ru/services/advertisinginterfacescomp/)
- [**Storybook**](https://lego-docs.s3.mds.yandex.net/story/@adv-interfaces/duplo/master/index.html)

## Установка

```bash
npm i @adv-interfaces/duplo --registry http://npm.yandex-team.ru
```

## Инфраструктура

Настроена сборка TypeScript в ES6, остальные файлы без изменений. Настроен eslint + prettier (со стандартными яндексовыми конфигами), запускаются на каждый коммит для измененных файлов. Настроен storybook.

```sh
# собрать TS в ES6 в папку dist
npm run build

# eslint --fix + prettier
npm run lint

# storybook
npm run storybook
npm run build-storybook
```

### Storybook

Storybook последнего релиза собирается и загружается в MDS S3
https://lego-docs.s3.mds.yandex.net/story/@adv-interfaces/duplo/master/index.html
