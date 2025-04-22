##Запуск
cd smarttv/alice/mm_backend && ya make -r --checkout && bin/manage.sh runserver localhost:8000

##Запросы (todo: заменить все это на pytest'ы)
###Переключение каналов
curl -v -d "@smarttv/alice/mm_backend/test/request.json" -H "Content-Type: application/json" -X POST http://localhost:8000/alice/channels/run

###Переключение входов
####Однозначный выбор
curl -v -d "@smarttv/alice/mm_backend/test/inputs-request.json" -H "Content-Type: application/json" -X POST http://localhost:8000/alice/inputs/run

####Многозначный выбор
Запрос №1
curl -v -d "@smarttv/alice/mm_backend/test/multiple-choice-input-request.json" -H "Content-Type: application/json" -X POST http://localhost:8000/alice/inputs/run

Запрос №2 (уточняющий)
curl -v -d "@smarttv/alice/mm_backend/test/multiple-choice-input-request2.json" -H "Content-Type: application/json" -X POST http://localhost:8000/alice/inputs/run
