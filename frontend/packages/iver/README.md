@yandex-int/iver
![Version](https://badger.yandex-team.ru/npm/@yandex-lego/iver/version.svg)
================


Пакет для работы с версионированием зависимостей в монорепозитории.
С помощью node api пакета можно:
- смотреть какие-то пакеты были затрону в vcs и в рамках каких коммитов, PR
- проставлять версии пакетам – ![Задача](https://badger.yandex-team.ru/st/ISL-9617/status.svg)
- обновлять зависимые пакеты – ![Задача](https://badger.yandex-team.ru/st/ISL-9617/status.svg)
- генерировать примечания к релизам – ![Задача](https://badger.yandex-team.ru/st/ISL-9618/status.svg)
- строить граф зависимостей – ![Задача](https://badger.yandex-team.ru/st/ISL-9623/status.svg)


# Использование
```bash
$ npm i @yandex-lego/iver
```

## Affected

Команда для вычисления измененных пакетов внутри lerna репозитория

```ts
import { Affected } from '@yandex-int/iver/'

(async()=>{
  // Задайте необходимые опции
  const options = {
      /** Опции для работы с vcs */
          vcs?: {
          /** С какого-то состояния vcs смотреть изменения
           * По умолчанию, Последний merge или Publish коммит
           */
          since?: string;

          /**
           * До какого момента считать изменения.
           * @default `HEAD`
           */
          till?: string;

          /**
           * Массив масок для игнора
           */
          ignore?: string[];

          /**
           * Сервис для работы с VCS.
           * Можно передать свой собственный адаптер.
           * По умолчанию используется адаптер для окружения (git или arc)
           */
          service?: VCS;
      },

      /**
       * Ссылка на корень монорепозитория.
       * По умолчанию вычисления средствами Лерны
       */
      root?: string;

      /**
       * Не показывать развернутую историю для пакетов, у которых версия не изменится.
       */
      noPrivate?: boolean;

      /**
       * Свой адаптер для Лерны.
       */
      lerna?: Lerna;
  }

  // Создайте экземпляр класса Affected
  const cmd = new Affected(options);

  // Получайте результат
  const { directs, dependent } = await cmd.execute();
})()
```

# How it works

## iver affected

> Вычисляем список измененных пакетов и файлов

Команда нужна для того, чтобы понять, что изменилось с момента последнего влития, чтобы проставить версии для измененных пакетов и опубликовать их в npm.

Работа команды в схематичном виде выглядит следующим образом:

<img src='https://jing.yandex-team.ru/files/axaxaman/affected.jpg'>
