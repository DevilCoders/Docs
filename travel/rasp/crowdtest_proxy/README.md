# Crowdtest proxy
Прокси запросов к внешнему балансеру crowdtest на внутренние тестинги - для тестирования асессорами.
https://st.yandex-team.ru/RASPFRONT-6219

Пример сборки и деплоя:
```
docker build -t crowdtest_proxy /Users/monitorius/work/rasp/crowdtest_proxy
docker tag crowdtest_proxy registry.yandex.net/rasp/crowdtest_proxy:latest && docker push registry.yandex.net/rasp/crowdtest_proxy:latest
```
Далее обновляемя на эту версию в https://platform.yandex-team.ru/projects/rasp/morda-front/crowdtest
