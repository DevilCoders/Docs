# react-ymaps

Готовый компонент для использования Яндекс.Карт внутри react приложения

# Установка

    npm i --save-dev @yandex-taxi/react-ymaps

# Зависимости

Необходимо установить плагин [@yandex-int/jsapi-v2-types](https://github.yandex-team.ru/maps/jsapi-v2.d.ts)
 для правильной работы тайпингов.

# Документация и примеры

https://github.yandex-team.ru/pages/taxi/react-ymaps/

# Документация Яндекс.Карт 

https://tech.yandex.ru/maps/doc/jsapi/2.1/quick-start/index-docpage/

# Разработка

Демо
    
    npm run guide

Линтинг
    
    npm run lint
    npm run test
    npm run fix

Релиз

    npm run prepare-release
    git push --follow-tags origin master && npm publish
    
