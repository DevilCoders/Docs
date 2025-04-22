Виснущая страница
<--delimiter-->
https://wiki.test.yandex-team.ru/hermiona/blocks/example-13/
<--delimiter-->
{{ toc }}

Для того, чтобы ваш сервис был доступен через протокол HTTPS, необходимо наличие валидных SSL-сертификатов.
Раньше пользователю было необходимо ((https://wiki.yandex-team.ru/cplb/howtocreatebalancer/#opcionalnozakazssl-sertifikatadljaservisa самостоятельно заказывать, готовить и подкладывать ssl-сертификаты.)) Теперь awacs позволяет пользователю оформить заказ сертификата нужного типа в ((https://crt.yandex-team.ru/ Сертификаторе)), подготовить его для использования программной поискового балансера, положить в ((https://yav.yandex-team.ru Секретницу)) и задать использование сертификата в нужной секции конфигурации балансировки.

Awacs позволяет заказывать сертификат при ((https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/ создании Namespace)) (при этом при ((https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/quick-start-mode/ создании в Quick-start)) режиме будет создан сертификат типа %%InternalCA%%). Эта инструкция посвящена работе с сертификатами в уже существующем Namespace на примере %%test-awacs-balancer.yandex-team.ru%%

//Примечание//. Сертификаты нужны только L7-балансерам. L3-балансер работает на более низком уровне (там не проверяют сертификаты). А от L7-балансеров до бэкэндов трафик идёт не шифрованный.

===(cert-create) Заказ и использование сертификата
====(cert-order) Заказ сертификата
Для заказа нового сертификата необходимо:
* на странице Namespace нажать ##Show certificates##
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts01.png
* на открывшейся странице сертифкатов текущего Namespace нажать кнопку ##Order certificate##
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts02.png
* на открывшейся странице параметров сертификата задать:
  * **Id** - идентификатор сертификата (по умолчанию совпадает с именем Namespace). Используется в дальнейшем в конфиге балансера
  * **Certificate authority type** - тип сертификата. Доступные варианты:
    * ##Internal## - внутренний сертификат InternalCA
    * ##External## - внешний продакшн сертификат от CertumProductionCA 
  * **Common name** - имя хоста, "защищенное" данным сертификатом
  * **Subject alternative names** - дополнительные (альтернативные) имена хостов, защищенные данным сертификатом
  * **ABC service responsible for this certificate** - сервис, владеющий данным сертификатом.
* после задания всех параметров (см. пример) необходимо нажать кнопку %%Submit%%
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts031.png
* после старта заказа сертификата на странице сертификата будет отражаться текущий статус заказа и взаимодействия с Сертификатором вплоть до завершения операции:
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts05.png
//Примечания//.
1. для внутренних продакшн сервисов (== в которые будут ходить только те, у кого в браузере установлен корневой сертификат Яндекса //YandexInternalRootCA//) или другие внутренние сервисы можно использовать InternalCA
2. awacs не указывает при заказе TTL сертификатов и использует значения по умолчанию (по состоянию на 01.09.2019 TTL для сертификатов типа Internal равен 2 года, для External - 1 год).
3. Заказ сертификата через API Сертификатора осуществляется от имени @robot-awacs-certs. После того, как Сертификатор выпускает сертификат и помещает его в Секретницу, awacs тем же роботом забирает оттуда сертификат, подготавливает его для балансера, и кладёт обратно в тот же секрет, откуда он потом штатными средствами Nanny доставляется на балансер. В этой схеме доступ к секрету с сертификатом имеют люди с ролью Управление Сертификатами из указанного ABC-сервиса, и сам @robot-awacs-certs. 

====(cert-view) Просмотр сертификата
После того, как cертификат успешно создан, он отображается в списке сертификатов вашего Namespace 
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts06-1.png

При выборе сертификата пользователю доступен просмотр основных параметров сертификата (вкладка %%Certificate info%%), включая срок окончания действия сертификата:
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts06.png
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts07.png

На вкладке %%Storage%% пользователь может идентификатор секрета в Секретнице и его ревизию:
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts08.png

====(cert-use) Использование сертификата в балансере
После того, как cертификат успешно создан, необходимо добавить его в конфигурацию **каждого** балансера вашего Namespace. Модификация конфигурации балансера зависит от режима, в котором он был создан:
* {[**для ((https://wiki.yandex-team.ru/cplb/awacs/quick-start/ quick-start режима))** необходимо в блок, соответствующий домену, для которого был заказан сертификат, добавить строку %%cert: cert_id%%, где %%cert_id%% — идентификатор сертификата, указанный при его заказе.
<{Пример
%%---
quick_start_balancer_macro:
  version: 0.0.1
  http: {}
  https: {}
  domains:
  - id: main
    matcher:
      hosts:
      - test-awacs-balancer.yandex-team.ru
      - test-awacs-balancer.in.yandex-team.ru
    cert: test-awacs-balancer.yandex-team.ru
    routes:
    - id: main
      matcher:
        path_prefix: /
      endpoint_sets:
      - cluster: sas
        id: test-stage.MultiClusterReplicaSet
%%}>]}
* {[**для easy mode режима** необходимо в %%l7_macro%% добавить блок %%https%% с идентификатором сертификата. О всех настройках l7_macro можно узнать в ((/cplb/awacs/top-level-easy-mode/ документации)).
<{Пример
%%
l7_macro:
  version: 0.0.1
  http: {}
  https:
    certs:
      - id: romanovich.in.yandex-team.ru
%%}>
]}
* {[для остальных режимов: необходимо добавить ((https://wiki.yandex-team.ru/cplb/awacs/cookbook/#kakpodkljuchithttpskmoemuservisu поддержку https)), если ваш балансер требует наличие ssl (если вы планируете использовать несколько ssl-sni-контекстов в балансере, ознакомьтесь с тем, ((https://wiki.yandex-team.ru/cplb/awacs/cookbook/#kakopisatneskolkosni-kontekstovdljahttps как добавить их поддержку)) <{Пример ((https://a.yandex-team.ru/arc/trunk/arcadia/infra/awacs/mirror/test-awacs-balancer.yandex-team.ru/balancers/test-awacs-balancer.yandex-team.ru_man.yml?rev=5436056#L40 конфига)) с https секцией
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts10-1.png
//Секцию ##https_section## я скопировал с ##http_section##.
Прописал %%port: [443]%%.
В секции ##extended_http_macro## %%port:%% не указывал.//
%%
https_section:
      ips: ['*']
      ports: [443]
      extended_http_macro:
        enable_ssl: true
        ssl_sni_contexts:
          test-awacs-balancer.yandex-team.ru:
            cert: !c test-awacs-balancer.yandex-team.ru
            servername_regexp: default      
        modules:
          - regexp:
              include_upstreams:
                filter:
                  any: true
                order:
                  label:
                    name: order
%%
//Не забудьте заменить %%test-awacs-balancer.yandex-team.ru%% на свои значения, общий вид секции ssl_sni_contexts должен быть//
%%
ssl_sni_contexts:
    <FQDN>:
        cert: !c <cert_id>
        servername_regexp: default
%% 
}>

===(cert-discard) Отзыв сертификата
Для отзыва сертификата необходимо перейти на страницу соответствующего сертификата и перейти во вкладку %%Delete%%
800x0:https://wiki.yandex-team.ru/users/pirogov/balancers/tutorial/certs/.files/awacscerts11.png

При этом пользватель может выбрать один из сценариев отзыва:
* **Remove only from awacs** - сертификат удаляется только из спеки в awacs, но остается в Секретнице и остается валиден
* **Remove from awacs and from storage (e.g. YaVault)** - сертификат удаляется и из awacs, и из Секретницы, но явно не отзывается
* **Revoke and remove from awacs and from storage (e.g. YaVault)** - сертификат явно отзывается в Сертификаторе и удаляется отовсюду.

===(cert-reorder) Перевыпуск сертификата
На текущий момент алгоритм перевыпуска сертификата следующий: за 30 дней до истечения сертификата awacs инициирует заказ нового, без уведомления пользователя. В UI процесс перезаказа отображён на странице сертификата, и выглядит точно так же, как обычный заказ сертификата. После того, как сертификат готов, он не применяется автоматически, вместо этого дежурный из команды awacs должен нажать в UI кнопку ##Unpause certificate renewal##, чтобы для этого конкретного сертификата включить автоматику. Это промежуточная схема на период обкатки механизма автообновления сертификатов. 
<{Окончательная схема
После того, как сертификат готов, он отлёживается сутки, после этого авакс автоматически записывает в спеку сертификата новую версию, и все балансеры, где он используется, обновляют архив с секретом.}>

Пока оригинальный сертификат ещё не истёк, в UI авакса есть кнопка ##Restore certificate from backup##, для антифакапных мер. Она заново применяет старую спеку сертификата (которая скоро истечёт), и отключает для этого сертификата автоматику обновления. Прежде чем нажать эту кнопку, пользователь увидит много красных предупреждений, что это рискованное действие, и после него надо будет идти в саппорт awacs, чтобы обновить сертификат. При нажатии кнопки в Sentry авакса прилетает сообщение об этом (и транслируется в телеграм команде awacs), команда уведомляется и дежурный сможет дойти до пользователя, чтобы понять причины операции восстановления старого сертификата.

Когда оригинальный сертификат окончательно истекает, он отзывается в сертификаторе и удаляется из секретницы, и кнопка ##Restore certificate from backup## пропадает из UI.

===(faq) Вопросы и ответы
====(access) У кого есть доступ к созданному сертификату?
Доступ к секрету с сертификатом имеет только робот @robot-awacs-certs. 

====(monitoring) Могу ли я следить за сроком действия сертификатов?
Awacs автоматически для всех балансеров создает джагглер-проверки %%check-enddate-certificate-instances%%, переходящие в состояние !!(red)CRIT!! за 2 недели до окончания срока действия сертификата
https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dcheck-enddate-certificate-instances%26tag%3Dtest-awacs-balancer.yandex-team.ru
