## Основной код и докер образ для аналитических ручек на flask

Flask c ручками живет здесь - http://analytics-metrika.in.yandex.net

## Холодный старт. Docker

1. Установка docker

    ```
    sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && sudo apt-get update && sudo apt-get install -y docker-ce
    ```
2. Добавить юзера в группу docker, кто будет запускать образ

    ```
    sudo usermod -a -G docker your-user-name
    После нужно будет перелогиниться
    ```
3. Токен для авторизации в Docker distribution

    https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1

4. Авторизации в Docker distribution

    ```
    docker login -u <login> --password-stdin registry.yandex.net
    Далее вводим токен в формате 
    <token_body><Enter>
    ^D(иногда может понадобиться еще один ^D, третий раз только не надо - выйдете из консоли)
    ```
5. Собираем образ из текущей папки
    ```
    docker build . --no-cache  --tag my-own-image --network host
    ```

6. Запускаем образ
    ```
    docker run -d --name my-own-container --network host -p 5000:80 --env YAV_OAUTH=<oauth_for_vault> my-own-image
    ```

7. Appendix 1. Полезные команды для докера
    ```
    docker logs my-own-container - посмотреть логи контейнера
    docker run --rm -it --entrypoint bash --network host my-own-image - запуск образа в интерактивном режиме
    docker cp . my-own-container:/app -  Скопировать файлы из текущего каталога в рабочую директорию образа
    docker exec -it my-own-container bash - Зайти в текущий контайнер в интерактивном режиме
    ```

## Запуск локально

    cd ~/arcadia/metrika/analytics/counter-code-analytics-flask
    python3 run.py --debug=1

## Как выложить новую версию

0. Запушить изменения в транк
1. Собарть проект - https://sandbox.yandex-team.ru/task/1162836456/view. Нужно апнуть версию в поле "Custom version". Текущую версию можно посмотреть в делое
2. Обновить образ в деплое. Достаточно указать новую версию проекта в поле "Tag name" - https://deploy.yandex-team.ru/stages/counter-code-analytics-flask/edit/du-prod/box-box#resources

## Как добавить страницу на виртуалку

* Локально отлаживаем страницу и после работающий код перенесем в проект
* Добавляем отдельную папку с основным кодом в [/files](https://a.yandex-team.ru/arc_vcs/metrika/analytics/counter-code-analytics-flask)
* Добавляем отдельную паку со статикой в [/templates](https://a.yandex-team.ru/arc_vcs/metrika/analytics/counter-code-analytics-flask/templates)
* Для новых страниц нужно наследоваться от общей страницы [idnex.html](https://a.yandex-team.ru/arc_vcs/metrika/analytics/counter-code-analytics-flask/templates/index.html). В ней уже прописаны все нужные ресуры и встроен счетчик метрики. Подробнее про наследование шаблонов можно почитать в [доке jinja](http://jinja.pocoo.org/docs/2.10/templates/#base-template)
* В [index.py](https://a.yandex-team.ru/arc_vcs/metrika/analytics/counter-code-analytics-flask/pages/index/index.py) добавляем страницу с описанием. После этого она появится в таблице на основной странице. Все ссылки ведут уже на платформу, локально работать не будут!
* В [run.py](https://a.yandex-team.ru/arc_vcs/metrika/analytics/counter-code-analytics-flask/run.py) прописываем импорт и адрес новой страницы

* Пример импорта новой страницы
```python
import clickhouse_login.main as clickhouse_login - импортируем скрипт, который генерит страницу

#Clickhouse Login
app.add_url_rule('/clickhouse_login', 'generate_ch_user', clickhouse_login.generate_ch_user, methods = ['GET', 'POST'])

параметры:
  адрес страницы,
  endpoint (кажется просто какая-то строковая переменная)
  функция которая генерит страницу
  **kwargs с опциями
```
