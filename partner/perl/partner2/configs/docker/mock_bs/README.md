# docker_mock_bs

Это микросервис, который делает мок ручки БК EditPage.

## Собрать-запустить

Для того чтобы собрать:

    docker build --tag mock_bs .

Для того чтобы запустить:

    docker run \
        --detach \
        --env START_PAGE_ID=2000 \
        --publish 1082:80 \
        --name mock_bs \
        mock_bs

После выполнения этих действи на порту 1082 будет работтать SOAP сервер с
моком ручки EditPage.

## Как работает мок

Пример запроса к ручке EditPage:

    {
        "0" : {
            "Description" : "masterseptika.ru",
            "Domain" : "masterseptika.ru",
            "IsYandexPage" : "0",
            "Name" : "masterseptika.ru",
            "PPCTotal" : "9",
            "PartnerID" : "904018",
            "Places" : {},
            "State" : "-1",
            "TargetType" : "3"
        }
    }

Пример ответа от ручки EditPage:

    {
        "0" : {
            "Error" : "0",
            "ErrorStr" : "",
            "PageID" : "2002"
        }
    }

В том случае если в запросе есть PageID, то в ответе будет этот PageID.

Если в запросе не было PageID, то мок будет возвращать числа, начиная с
START_PAGE_ID. Т.е. если при старте контейнера указать START_PAGE_ID=2000,
а потом сделать несколько запросов без PageID, то в ответах будудут следующие
PageID: 2000, 2001, 2002, ...

Мок никак не проверяет те данные, которые передаются в запросе.

Контенер с моком ведет логи запросов ответов, если сделать
`docker logs -f mock_bs` то будут видны все запросы к этому моку и его ответы.

## Примеры ответов БК

Пример успешного ответа:

    {
        '0' => {
            'Error' => '0',
            'PageID' => '149250',
            'ErrorStr' => ''
        }
    }


Пример ответа с ошибкой:

    {
        '0' => {
            'Error' => '12',
            'PageID' => '107957',
            'ErrorStr' => 'TargetType can\'t be changed from 3 to 0'
        }
    }
