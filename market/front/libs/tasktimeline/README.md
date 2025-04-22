# tasktimeline

Сервис генерации svg картинки, визуализирующей прохождение задачи по статусам

Для разработки необходимо задать переменную окружения TOKEN стартека (https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b) 

npm run dev запускает сервер

Скрипт publish создает docker образ с версией из package.json и добавляет его в репозиторий. Из этого образа можно разворачивать сервис в Ya.deploy

Подробнее про докер образы и репозиторий https://wiki.yandex-team.ru/qloud/docker-registry

Имеющиеся версии в репозитории можно посмотреть https://wiki.yandex-team.ru/qloud/docker-registry/#polucheniespiskategovvrepozitorii

- /task/MARKETFRONT-17582/svg Отображает svg
- /task/MARKETFRONT-17582/svg/attach Прикрепляет svg к задаче
