# Communication proxy

### Локальный запуск

- Для сборки проекта необходимо запустить скрипт `./generate_project.sh` лежащий в корне репозитория (После этого перегенерировать проект можно будет через соответствующую конфигурацию в IDEA)
- Для дальнейшего запуска можно использовать сгенерированную кофигурацию в IDEA `Run Service (generated)`. Для локального запуска необходимо в Environment variables прописать [**mbi.tvm.client.secret**](https://yav.yandex-team.ru/secret/sec-01dq7mcmp61rc6d169efvdyhas/explore/version/ver-01dq7mcmvwrdz6jgc04ncbt00k) и [**tvm.client.secret**](https://yav.yandex-team.ru/secret/sec-01fpaer8kkmrn2ssqfjnmnj64y/explore/version/ver-01fpaer8kxrm3fyz0v2kgfpjne), 
доступ к секретницам можно запросить через IDM. Это костыль который уедет в рамках https://st.yandex-team.ru/MBI-76239. 
![https://jing.yandex-team.ru/files/shashulovskiy/Screen%20Shot%202022-01-19%20at%2013.15.12.png]()

### Документация по проекту

https://wiki.yandex-team.ru/mbi/newdesign/components/communication-proxy/


### Сервис в ABC 

https://abc.yandex-team.ru/services/communication-proxy/
