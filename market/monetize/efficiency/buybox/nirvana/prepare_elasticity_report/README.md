Код по генерации графа для определения 10 точек "хорошей" эластичности, которые поедут под репорт. Используется в байбоксе.

Хитман процесс: https://hitman.yandex-team.ru/projects/market\_dp\_buybox/elasticity\_buybox

Автоматическая выкатка пока не сделана, будет готова тут https://st.yandex-team.ru/MDP-1196 . Пока механизм выкатки такой, заходим в папку graph, собираем ya make . Далее вызываем ./local\_run.sh скрипт сгенерит граф в тестовый воркфлоу, прописав туда пути до последних таблиц эластичности, запускаем и сверяем с тем, что в проде. Если в тесте все норм, запускаем ./prod\_run.sh. Дополнительно потребуется создать у себя локальный файл ~/.vhrc и положить туда строчку --oauth-token=ваштокеннирваны.
