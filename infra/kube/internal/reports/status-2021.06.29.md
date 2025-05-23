# Status report 29.06.2021
## Auth
Детали: [KUBERTC-2](https://st.yandex-team.ru/KUBERTC-2).
Сделали первый простой подход: kube-webhook.
В первом приближении работает. Использовали в Няне (см. ниже). Дальнейшие векторы развития примерно понятны:
  * auth proxy для web приложений
  * staff-sync в k8s (для независимости от доступности staff'а)
Заниматься пока не планируем.

## Crossplane
Детали:
  * [KUBERTC-5](https://st.yandex-team.ru/KUBERTC-5)
  * [KUBERTC-7](https://st.yandex-team.ru/KUBERTC-7)

Конкретно мы разбирались/исследовали [crossplane/provider-azure](), а не универсальной частью [crossplane/crossplane], которая пытается давать сервисы, абстрагированные от конкретных облаков.

Текущий итог:
  * Подход - рабочий.
  Мы одним инструментом можем поднимать различную инфраструктуру
  * Подход - удобный.
  Инженер, незнакомый с Azure и k8s, выбирает работать с этим через YAML, а не через дебри `az` CLI или веб:
```
Vasiliy Pahomov, [29.06.21 17:44]
kubectl yaml удобнее. меньше действий
* поправил yaml
* kubectl apply
* kubectl describe (ему бы еще побыстрее отрабатывать, хз че он такой грустный)

Vasiliy Pahomov, [29.06.21 17:45]
console кстати не пробовал, а в web хер че найдешь куча разных страничек и формочек. А еще если нужно что-нибудь пересоздать, то вообще беда завново все натыкивать
```
  * Библиотека контроллера сильно помогает, срезать кучу бойлерплейта по обработке событий и организации кода.
  С ней быстро разобрался разработчик невысокого грейда.
  * Конкретная реализация provider-azure:
    * очень неполная (банально нет просто VM)
    * мало активности (например, [PR#270](https://github.com/crossplane/provider-azure/pull/270)).
  * Облака в целом это очень сложно и непривычно. Многие ожидания, к которым привыкли внутри - не работают. См. раздел VPN ниже.

**Дальнейшие планы** прямо сейчас:
  * Поднять Azure Kubernetes Service через наш crossplane. Чтобы познакомиться с особенностями работы с контейнерами, сетями, реестрами.

## nanny + kube
Запустили аллокации через k8s api server:
```
❯ kubectl --context nanny-dev get allocations
NAME                           TYPE         AUTHOR      AGE
reddi-test-mc                  YP_POD_IDS   anonymous   6d
reddi-test-yp-5-copy-reddi-2   YP_POD_IDS   reddi       6d

❯ kubectl get allocations
NAME              TYPE         AUTHOR    AGE
production-orly   YP_POD_IDS   nekto0n   4d
reddi-test-yp-3   YP_POD_IDS   reddi     4d1h
```
Из плюсов:
  * Осваиваем культуру класть конфиги в репозиторий (gitops?): [k8s-nanny-stuff/rbac](https://a.yandex-team.ru/arc/trunk/arcadia/infra/k8s-nanny-stuff/rbac).
  Настройки доступов - это обычные объекты, работать с которыми можно так же как с любыми другими (`kubectl diff/apply`).
  * CLI получили "на сдачу".
  * Инструментарий/возможности отладки и т.д (после соотв освоения) в общем нравятся инженерам:
```
nekto0n, [29.06.21 17:45]
Привет! А можешь какой-то отзыв дать про k8s по итогам работы в таком ключе с ним? Типа: Божественно/круто/сойдёт/отвратительно/зачтомнеэто.

Evgeny Chekalov, [29.06.21 18:02]
привет! мне очень понравилась связка CRD + client-go +  kubectl, один только страх, что дальше это перестанет натягиваться на нашу модель, но очень бы хотелось продолжить
```
Из минусов:
  * Поднять k8s нет никаких проблем. Поднять его в корректном для production'а режиме - более сложная задача.
  Тут есть огромный опыт у Внешнего Облака.
  * Многие инструменты k8s'а на самом деле недоделаны, in progress, либо deprecated.
  * По ключевым нашим задачам области малодокументированы, но интерес в этой области большой и сообщество очень активно.

Дальнейшие шаги:
  * Пока нет - ребята перешли на другие аспекты задачи (бизнес логика и внедрение).


## awacs + kube
Обсудили с ребятами шаги для максимального быстрого получения чего-то законченного для интеграции awacs + k8s. Т.е. чтобы `kubectl apply` можно было сделать и получить видимые изменения. Это поможет оценить применимость на всём пути (работа с API/библиотеками, натягивание модели awacs, пути плавной миграции и т.д.).

Дальнейшие шаги:
  * Ребята в фоновом режиме почитают про k8s и [kubebuilder](https://book.kubebuilder.io/) и попробуют добавить `DNSRecord`, которые можно создавать в AWACS.

## VPN
Детали:
  * [KUBERTC-8](https://st.yandex-team.ru/KUBERTC-8).
Оказалось, что штатно у тебя нет сетевой связности с сетями твоих публичных облаков. Это объяснило многие архитектурные решения k8s. Например, доступ в контейнеры пода через kubectl с проксированием через api-server и т.д.

Штатного решения (имеется ввиду СИБ/НОК) для текущих ребят, которые пытаются запускаться во внешних облаках нет. Мы немного потратили времени на исследование технических возможностей, что можно предложить пользователям. Взяли самый простой инструмент - [wireguard](https://www.wireguard.com/). Это простая в эксплуатации, кросплатформенная (вплоть до возможности вкомпилировать в своё приложение), но безопасная реализация туннелей. Оно поднимается, настраивается односторонняя связность (т.е. через NAT на gateway виртуалке).

Дальнейшие шаги:
  * Дизайн схемы настройки туннелей до нужного облака на рабочих станциях разработчиков через что-то вроде `kubectl yandex vpn -n toloka-azure`.
  * Аудит от СИБ.
  * Документация к тому, что и как удавалось настроить.
