# page_id_generator

https://wiki.yandex-team.ru/partner/w/partner2-intapi-get-next-page-id/

## Как запустить локальную версию этого проекта

 1. Нужно поставить docker
 1. Склонировать этот репозиторий
 1. В папке с кодом из этого репозитория запустить `./restart`
 1. Дождаться пока все собереться
 1. После того как все собереться сервис будет работать на http://127.0.0.1

## Пример использования

    $ curl -X "POST" "http://127.0.0.1/intapi/get_next_page_id?service=partner" ; echo
    {"page_id":"320006"}

## Как собрать и выложить релиз

 1. Проверить что другие люди не собирают релиз анкеты
 1. Замержить задачу (или задачи) в master
 1. Переключить рабочую копию на текущий master
 1. Перезапустить систему `./restart`
 1. Прогнать тесты `./check` — все тесты должны быть зеленые
 1. Поправить файл `./build` — раскомментировать и указать значение для VERSION. Значение — это текущая дата, плюс номер сборки за этот день (смотреть в deploy какие уже были)
 1. Запустить `./build` — он соберет докерный образ
 1. Выполнить команды которую выдал `./build`
 1. Выложить образ в тестовое окружение deploy — https://deploy.yandex-team.ru/stages/page-id-generator-test
 1. Проверить работу анкеты на ТС `curl -X "POST" "https://utils.partner2-test.yandex.ru/intapi/get_next_page_id?service=direct"`
 1. Если все ок, то выложить образ в прод окружение deploy - https://deploy.yandex-team.ru/stages/page-id-generator-prod
