enb-tanker
==========

Данный пакет позволяет получать кейсеты из танкера по заданным настройкам. Работает быстрее, чем lego/tools/get-tanker.js, и, почему-то, работает в тех случаях, когда get-tanker в lego возвращает пустые кейсеты.

Установка
=========

Т.к. пакет содержит ключ из танкера, я не стал выкладывать его в публичный npm (а во внутренний не стал, т.к. он часто падает).

Прописываем зависимость в `dependencies` package.json нашего проекта:

```javascript
"enb-tanker": "git://github.yandex-team.ru/enb/enb-tanker.git#master"
```

Устанавливаем командой:

```
npm install
```

Теперь подключаем в наш `.bem/enb-make.js`:

```javascript
module.exports = function(config) {
  // ...
  config.includeConfig('enb-tanker/enb-make');

  config.setEnv({
      TANKER_PRJ: 'my-project',
      TANKER_HOST: 'tanker-test.yandex-team.ru', // или tanker-api.tools.yandex.net
      TANKER_MAX_ATTEMPTS: '10', // опцианально, количество попыток запроса при ошибке танкера
      TANKER_PRJ_REV: 'master',
      TANKER_API_TOKEN: 'cd15e769d0184cdf9e064918b3bb7dec' // опцианально, токен, если отличается от стандартного
  });
};
```

Собственно, все. Теперь можно загрузить кейсеты:

```
./node_modules/.bin/enb make i18n.get
```

Дополнительные возможности
==========================

Для того, чтобы избавиться от полных путей (через двоеточие и подчеркивание), enb-tanker поддерживает опции:

    I18N_BLOCK_NAME — имя блока для сохранения кейсетов.
    I18N_MODIFIER_NAME — имя модификатора.
    I18N_LEVEL_PATH — путь к уровню переопределения.
    I18N_KEYSET_DOWNLOAD_OPTS — querystring, настройка дополнительных параметров для закачки keyset'ов. (например: "all-form=true&status=unapproved")

После установки опций, i18n.get будет класть кейсеты (в имени которых отсутствует двоеточие) в директорию, сформированную на основе данных опций.
