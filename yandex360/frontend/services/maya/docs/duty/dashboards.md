# Графики

Для риалтаймовых графиков мы используем yasm, он же Голован ([дока](https://doc.yandex-team.ru/Search/golovan-guide/concepts/about.xml), [вики](https://wiki.yandex-team.ru/golovan/)).

Есть несколько уже готовых дашбордов:
* [Основной дашборд maya](https://yasm.yandex-team.ru/panel/pistch.maya_public_brief/)
* [MODEL_REJECTED maya](https://yasm.yandex-team.ru/panel/pistch.maya_public_model-rejected/)
* [Основной дашборд maya-corp](https://yasm.yandex-team.ru/panel/pistch.maya_corp_brief/)
* [MODEL_REJECTED maya-corp](https://yasm.yandex-team.ru/panel/pistch.maya_corp_model-rejected/)

На основном дашборде приведены графики с ключевыми показателями. На них обычно можно увидеть почти любую проблему,
если знать, куда смотреть. За расследованием чаще нужно обращаться к более детальным графикам (MODEL_REJECTED, например),
[логам](logs/README.md) или же делать собственный график.

## Как сделать новый график

1. Открыть [Голован](https://yasm.yandex-team.ru)
2. В поле "Контекст" ввести контекст графика.

 Для показателей с инстансов maya:
```
itype=qloud;
hosts=QLOUD;
prj=mail.maya[-corp].production;
signals={{имя_сигнала}}
```

Более подробно про синтаксис контекста графиков - в доке голована (или можно подглядеть, как сделаны графики на уже существующих дашбордах).

## Что можно увидеть в Головане?

* Всё то, что отправляет туда сам qloud (данные от porto, примеры можно увидеть в дашбоде qloudного окружения) - использование ресурсов
* Неудачи http-клиента Даффмана:
    * таймауты (`unistat-http-{{BACKEND_FQDN}}_timedout_dmmm`);
    * фейлы (`unistat-http-{{BACKEND_FQDN}}_failure_dmmm`);
    * MODEL_REJECTED (`unistat-custom_duffman_model_rejected_{{MODEL_NAME}}_dmmm`);
* Неудачи http-сервера Даффмана:
    * совсем не смогли сформировать ответ (`unistat-custom_auth_error_dmmm`)
    * ошибка авторизации (`unistat-custom_route_common_request_error_dmmm`)
    * всё, что добавим в процессе (отправим через `core.yasm`)
* Клиентские ошибки с разбиением по типу и имени:
    * с именем (`unistat-monitoring_error_{{TYPE}}_{{NAME}}_dmmm`);
    * без имени (`unistat-monitoring_error_{{TYPE}}_dmmm`);
* Коды ответов и тайминги от nginx внутри контейнера:
    * коды ответов моделей (`unistat-nginx_maya_models_{{MODEL_NAME}}_{{HTTP_CODE}}_count_dmmm`, `unistat-nginx_maya_models_{{MODEL_NAME}}_{{1/2/3/4/5}}xx_count_dmmm`);
    * коды ответов индексной страницы (`nginx_maya_index-page_{{1/2/3/4/5}}xx_count_dmmm`);
    * коды ответов старого интерфейса (`nginx_cal_request_{{1/2/3/4/5}}xx_count_dmmm`);
    * тайминги отдельной модели (`nginx_maya_models_time_{{MODEL_NAME}}_hgram`);
    * тайминги индексной страницы (`nginx_maya_index-page_time_hgram`).
    
С помощью агрегирующих функций и комбинации сигналов можно получить графики, показывающие какую-то конкретную,
узкоспецифичную проблему.
