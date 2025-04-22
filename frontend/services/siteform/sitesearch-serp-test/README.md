# sitesearch-serp-test

Приложение для тестирования выдачи ПДС. Тут есть nginx и несколько статических страничек, на которых можно проверить выдачу, «вставленную на сайт». См. [Dockerfile](Dockerfile).

Можно легко задеплоить изменения такой командой:


```
 ./deploy.sh
```

Она соберёт докер-образ и раскатает его в нужные кулаудные окружения. См. [deploy.sh](deploy.sh). Список окружений см. в папке [qloud-configs](qloud-configs).

---

Related links:

- [SITESEARCH-3448: Тесты на поисковую часть ПДС](https://st.yandex-team.ru/SITESEARCH-3448)
- [Окружение в Qloud](https://platform.yandex-team.ru/projects/sitesearch/sitesearch-serp-test)
