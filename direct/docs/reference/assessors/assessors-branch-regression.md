# Запуск регрессии на асессоров в бранче

{% note alert %}

**Стенд для асессоров:** [https://branch.crowdtest.direct.yandex.ru/dna/grid/campaigns](https://branch.crowdtest.direct.yandex.ru/dna/grid/campaigns)   
На морду они зайти не смогут пока не сделано [DIRECT-160904](https://st.yandex-team.ru/DIRECT-160904#61ea6a5b8a8d4702d2e18f0e)

{% endnote %}

#### Создаем бету
Бета должна смотреть в базу ТС, так как все тестовые данные для асессоров живут именно там

#### Изменяем бранч в настройках бекенда и апстрима в awacs
1. Переходим на вкладку [Show backends](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/crowdtest.direct.yandex.ru/backends/list/) и жмём на иконку редактирования **рядом с хостом branch.crowdtest.direct.yandex.ru** 

   {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-02-02_15-25-11.png "скрин")

   {% endcut %}

2. Переходим по ссылке _Create or edit current endpoint set_

   {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-02-02_15-31-32.png "скрин")

   {% endcut %}

3. Заполняем поля
- **Host** - заменяем на хост своей беты
- **Port** - 443
- **Weight** - 1
- **IPv6 address** - нужно выяснить с помощью команды host
```bash
> host 13933.beta6.direct.yandex.ru

ppcdev6.yandex.ru has IPv6 address 2a02:6b8:0:144d:e330:c2df:61ee:2744
```

   {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-02-02_15-35-26.png "скрин")

   {% endcut %}

4. Жмём Save и ждём, пока на странице списка бекендов всё позеленеет. Это значит что бекенд обновлен
5. Переходим на вкладку [Show upstreams](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/crowdtest.direct.yandex.ru/upstreams/list/) и жмём на иконку редактирования **рядом с апстримом branch** 

   {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-02-02_15-39-14.png "скрин")

   {% endcut %}

6. В Spec заменяем в поле value хост на свою бету из п.3 и жмем Save

   {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-02-02_15-40-00.png "скрин")

   {% endcut %}

7. Далее ждём, пока на странице списка апстримов всё позеленеет и проверяем что стенд работает. Заходим на [https://branch.crowdtest.direct.yandex.ru/dna/grid/campaigns](https://branch.crowdtest.direct.yandex.ru/dna/grid/campaigns) и проверяем по логам, что запросы летят в вашу бету  
Временно чтобы убедиться, что стенд смотрит на новую бету, можно открыть морду [https://branch.crowdtest.direct.yandex.ru](https://branch.crowdtest.direct.yandex.ru) - с нее должно средиректить на бету (но эта возможность скоро пропадет)

#### Запускаем задание на асессоров
1. Создаем тикет на регрессию [по шаблону](https://st.yandex-team.ru/createTicket?template=8355&queue=DIRECTAS)
Добавить шаблон себе можно [по ссылке](https://st.yandex-team.ru/settings/templates/issues?name=Тестирование%20регрессии%20в%20бранче&owner=1120000000014295&queue=DIRECTAS)
2. В названии тикета указать свой бранч
3. Далее продолжаем [с п.3 инструкции ручного запуска](regression-assessors.md)
4. **Бронь для запуска на шаге 10 создать новую!** Регулярную не используем под запуски в бранчах!
