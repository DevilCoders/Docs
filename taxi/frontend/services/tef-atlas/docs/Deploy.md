0. После закрытия PR и мёржа ветки в мастер, по готовности катить мёржим мастер в стэйбл
1. В актуальный stable заливаем актуальный master
2. Из корня проекта запускаем ./qloud/ideploy.sh
3. Выбираем контейнер (static / api / node), и, только для api или node, нужный стенд (testing / stable). Дальше соглашаемся
4. Идём на тестовый стенд [qloud-testing](https://qloud-ext.yandex-team.ru/projects/taxi-tools/atlas/testing)
5. Жмём Update на нужном компоненте

![](https://jing.yandex-team.ru/files/eugenest/taxi-toolsatlastesting_2019-06-04_17-52-19-acw9v.png)

6. Выбираем нужную версию 

![](https://jing.yandex-team.ru/files/eugenest/taxi-toolsatlastesting_2019-06-04_17-53-54-rkf7p.png)

7. Дожидаемся раскатки, тестируем задачи
8. Создаём релизный тикет в очереди TAXIREL — https://st.yandex-team.ru/createTicket?queue=TAXIREL. Обязательно указываем:
    1. В заголовке указываются версии затронутых компонентов и соответствующие им версии. Например: Atlas-frontend: static-1.4.57, api-1.0.12
    1. Обязательно добавляются в связанные те st-задачи, которые попали в релиз
    1. Призываются [окающие](./OkList.md) (по одному из каждой группы)
9. Идём на продовый стенд [qloud-stable](https://qloud-ext.yandex-team.ru/projects/taxi-tools/atlas/stable)
10. Жмём Create Draft
 
![](https://jing.yandex-team.ru/files/eugenest/image6.png)

11. Жмём Edit на том компоненте (компонентах), которые хотим обновить

![](https://jing.yandex-team.ru/files/eugenest/image4.png)

12. Выбираем нужную версию, нажимаем Save

![](https://jing.yandex-team.ru/files/eugenest/image5.png)

13. Жмём **prepare**. На этом этапе обязательно указываем в поле Comment ссылку на релизный тикет в TAXIREL

Разница между commit и prepare ([здесь](https://wiki.yandex-team.ru/qloud/doc/environment/) подробнее):

> COMMITTED - версия сохранена, полностью отвалидирована и готова к развертыванию, но аллокация ресурсов не проводилась, топология пустая.

> PREPARED - Все необходимые файлы для контейнера скачаны на хост (образ, сендбокс-ресурсы, секреты и пр.). Инстансы готовы к старту.

![](https://jing.yandex-team.ru/files/eugenest/image3.png)

14. После того, как релизный тикет окнули оба окающих, окнувший разработчик деплоит драфт. Автор драфта не может сам его катать. Это ограничение нужно для аудита.

![](https://jing.yandex-team.ru/files/eugenest/image2.png)

15. Закрываем релизный тикет

---

Внешний регламент выглядит так https://wiki.yandex-team.ru/users/eugenest/efficiency-frontend-atlas-releases/
