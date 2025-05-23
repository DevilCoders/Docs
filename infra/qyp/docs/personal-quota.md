# Персональная квота

## Цель {#aim}

Уменьшение времени, требуемого для создания виртуальных машин (ВМ) для разработчиков Поискового портала, за счет устранения для них процедуры заказа и подтверждения квот.

{% note info %}

Ресурсы в рамках персональной квоты не являются дополнительным бонусом к выданным ранее ресурсам, персональная квота — это гарантия возможности получения соответствующего объема ресурсов под задачи разработки.

{% endnote %}


## Описание {#description}

* Создается виртуальный ABC сервис (далее `pers_quota_srv`), в который входят все разработчики Поискового портала.
* Квота `pers_quota_srv` физически разделяется на набор полокационных квот `pers_quota_srv_locX`, сумма которых равна общим ресурсам квоты.
* Размер квоты на одного сотрудника фиксируется в виде конфигурационных настроек лимитов персональной квоты `pers_quota_limits`.
* Для предотвращения возможности перерасхода квоты (например, разработчик X создает N виртуальных машин) вводится дополнительное ограничение на одного пользователя (по логину) из виртуального сервиса на доступные для заказа ресурсы (см. далее).
* Работа Бизнес-юнитов планируется по прежней модели (квота на сервис, определяемая объемом переданных в сегмент dev ресурсов).


## Размеры персональных квот {#quota-preset}

Квотируемые ресурсы:
* CPU: `8c`
* RAM: `50GB`
* Disk (SSD): `300GB`
* Disk (HDD): `600GB`


## Типовые конфигурации ВМ {#typical-config}

Для упрощения работы при заказе ВМ, предлагается пользователю выдавать фиксированный набор preset'ов конфигураций ВМ (см. выше в таблице [Размеры персональных квот](#quota-preset)), должна быть возможность использования персональной квоты разово, а также по частям (например, в конце года пользователь в рамках персональной квоты может заказать либо одну ВМ размерами 8-50-300, либо набор ВМ из конфигураций меньшего размера в разных сочетаниях, но суммарно не превышающих размера персональной квоты).

## Workflow {#workflow}

* Пользователь в vmctl/UI инициирует запрос на создание ВМ (create)/аллокацию ресурсов (allocate), при этом в параметре ` --abc ` у него есть возможность указать варианты:
    * `personal`
    * `abc_id`
* Если пользователь выбирает ` personal ` и у него в ` --node-segment ` выбран сегмент ` dev `, то выполняется проверка его вхождения в состав ` pers_quota_srv `
    * Если пользователь не входит в сервис, за счет ресурсов которого обеспечена персональная квота, то выводится сообщение об ошибке: ` You have to be an employee of the <ServiceName/ProjectName> service/project in order to use its quota! `
    * Если проверка проходит (логика далее работает только для сегмента ` dev `):
       * Из YP получаем данные по ресурсам по всем выданным квотам abc-сервисов, в которые входит текущий пользователь (` accounts\spec.other\resource_limits `). Данные ресурсы делим на число пользователей, входящих в соотв. сервисы, суммируем результат и по каждому из ресурсов получаем значение ` <Объем использованного ресурса X> `:

          $\hbox{<Объем использованного ресурса X>} = \sum\limits_{i=1..n} \frac{R_i(X)}{Q_i}$

Где:

$n$ — число abc-сервисов с выданными в YP квотами, в состав участников которых входит пользователь

${R_i}$ — объем ресурса X, выданного в рамках квоты на сервис i

${Q_i}$ — число сотрудников сервиса i
    
* По каждому ресурсу (CPU, RAM, HDD, SSD) выполняется проверка вида `<Объем использованного ресурса X> + <Объем запрошенного ресурса X>` `<=` `<Объем ресурса X, доступного по персональной квоте>`
* Если оставшихся ресурсов недостаточно, выводим сообщение об ошибке `There are no resources available in you personal quote!` `Required: XX core(s), YY RAM, ZZ HDD/SSD. Available: AA core(s), BB RAM, CC HDD/SSD!`
* Если ресурсов достаточно - формируем запрос на создание ВМ/аллокацию ресурсов в YP:
* Если пользователь выбрал вариант `ANY ` при указании локации (пререквизитом является [QEMUKVM-407](https://st.yandex-team.ru/QEMUKVM-407)), то отправляем запрос в наиболее обеспеченный ресурсами локационный YP в разрезе квоты `quota_srv` (для проверки доступных ресурсов по локациям ориентируемся на запись в таблице <https://yt.yandex-team.ru/yp-vla/navigation?path=//yp/db/accounts&offsetMode=key>). Приоритет по типу ресурсов: `CPU > RAM > Disk`.



## Требования по визуализации {#pers-quota-srv}

У пользователя `pers_quota_srv` должна выводиться статистика по его потреблению ресурсов в рамках персональной квоты (<https://st.yandex-team.ru/QEMUKVM-243>, <https://st.yandex-team.ru/INFRAUX-76>)


## FAQ {#faq}

### Возможно ли использование как групповых, так и персональных квот? {#group-pers}

Возможно одновременное использование как групповых, так и персональных квот. Однако, при этом стоит учесть влияние групповых квот на доступный к использованию размер персональной квоты — размер персональной квоты [уменьшается](#workflow) на долю ресурсов, выданных в виде групповых квот, приходящуюся на одного сотрудника соответствующего ABC-сервиса (соответствующие ресурсы считаются уже израсходованными в рамках персональной квоты).


### Преобразование персональных квот в групповую {#change-group-pers}

Возможен вариант взаимозачета персональных квот в пользу групповой квоты (например, если сотрудникам подразделения в силу сервисной специфики для отладки необходима общая коммунальная виртуальная машина). В этом случае формируется [запрос на выдачу сервисной квоты в YP](https://wiki.yandex-team.ru/yp/quotas/), при этом в поле ` Если сервис переезжает - откуда? ` необходимо: 

  1. зафиксировать что квота компенсируется персональными квотами 
  2. указать сервис, на которых выдается групповая квота.

Исходя из размера персональной квоты на момент подачи заявки, а также числа сотрудников сервиса, на указанный сервис будет выдан объем ресурсов, представляющий собой разницу между объемом уже выданных ресурсов и суммой ресурсов, положенных указанному числу сотрудников по персональной квоте.

{% note info %}

Данный вариант заказа групповых квот работает только для сервисов Поискового портала!

{% endnote %}



### Что делать с людьми, чьи ВМ, поднятые в рамках сервисной квоты, уже превышают лимиты по персональной квоте? {#overlimit}

Оставляем их работать в рамках групповой квоты


### Что делать, если я попал в состав сервиса в качестве консультанта (не по задачам разработки) и на меня аккаунтится часть групповой квоты сервиса в QYP в сегменте dev {#pers-accounts}

Владелец сервиса может точно указать список лиц, имеющих право использования квоты в dev (Development) сегменте. Для этого необходимо выдать соответствующим сотрудникам роль ` Пользователь QYP ` в целевом сервисе. После этого, групповая квота не будет "аккаунтится" на пользователей сервиса, не имеющих роли ` Пользователь QYP `.

{% note warning %}

Если в сервисе **нет ни одного пользователя** с ролью `Пользователь QYP`, действует прежний механизм расчета "вычетов" из персональных квот сотрудников сервиса.

{% endnote %}


## Эксперимент по отказу от персональной квоты {#rejection-exp}

Подробнее <https://clubs.at.yandex-team.ru/infra-cloud/2029>

Актуальный список подразделений, персональная квота которых уже приватизирована:

1. Ответственный за ресурсы [@avitella](https://staff.yandex-team.ru/avitella):
    * [Умные устройства](https://staff.yandex-team.ru/departments/yandex_search_tech_quality_robot)
    * [Отдел базового качества Алисы](https://staff.yandex-team.ru/departments/yandex_main_searchadv_ai_dep71284)
1. Ответственный за ресурсы [@mvel](https://staff.yandex-team.ru/mvel):
    * [Департамент технологий портала](https://staff.yandex-team.ru/departments/yandex_main_searchadv_dep85477) **кроме**:
       * [Служба разработки рантайма новой БК](https://staff.yandex-team.ru/departments/yandex_search_tech_quality_component_8875_dep38743/)
       * [Отдел разработки баннерной системы](https://staff.yandex-team.ru/departments/yandex_monetize_banner/)
       * [Толока](https://staff.yandex-team.ru/departments/yandex_search_tech_assesment_toloka/)
       * [Служба инфраструктуры рекомендательных систем](https://staff.yandex-team.ru/departments/yandex_search_tech_quality_component_8875_dep29963/)
       * [Отдел Research](https://staff.yandex-team.ru/departments/yandex_main_searchadv_ai_9078/)
       * [Отдел базового качества Алисы](https://staff.yandex-team.ru/departments/yandex_main_searchadv_ai_dep71284)
       * [Отдел NLP](https://staff.yandex-team.ru/departments/yandex_search_tech_correct/)
    * [Управление поисковых продуктов](https://staff.yandex-team.ru/departments/yandex_search_tech_sq/) **кроме**:
       * [Сервис Яндекс.Кью](https://staff.yandex-team.ru/departments/outstaff_3210_dep21764)
       * [Группа B2B продукта](https://staff.yandex-team.ru/departments/yandex_search_tech_sq_dep70737)
