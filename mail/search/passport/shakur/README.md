##### API
/api/shakur/checkpassword
##### Get формат запроса
* &sha1=xxxx&sha1=yyyy - список sha1 для проверки

##### Post формат запроса
Тело запроса: 
`{"sha1":["xxxx", "yyyy"]}`

##### Формат ответа
`{
    "found": true,
    "passwords":[
        {"freq": 1, "source": "typeofdatabase", "sha1": "D80A2DE0126B5F475DA37E1556EED9A77BB0338E"}
    ]
 }`
 
##### Графики 
* https://yasm.yandex-team.ru/panel/vonidu.shakur_proxy_prod
* https://yasm.yandex-team.ru/template/panel/ps_search_backend/ctype=prod;prj=shakur/

