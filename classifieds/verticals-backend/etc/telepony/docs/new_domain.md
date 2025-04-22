## Инструкция разработчику для заведения нового домена
**_Важно_! Всюду по тексту ниже `new_domain`/`NEW_DOMAIN` (в т.ч. в составе названий переменный, путей и т.п.) нужно заменить на реальное название нового домена!**

1. БД:
   1. Добавляем домен в базу `INSERT INTO domain VALUES ($next_id, 'new_domain');` в тестинге и проде
2. Секретница:
   2. Добавляем секреты для mts_crm в [тестинге](https://yav.yandex-team.ru/secret/sec-01dh1qd9kbe37kh1ngaggdcjss/explore/versions)
   ```
   telepony_domain_new_domain_mts_crm_password=new_domain-testing
   telepony_domain_new_domain_mts_crm_password=new_domain
   ```
   2. Добавляем секреты для mts_crm в [проде](https://yav.yandex-team.ru/secret/sec-01dh1qerwf9mq0ykx48q9wdn1d/explore/versions)
   ```
   telepony_domain_new_domain_mts_crm_password=new_domain-stable
   telepony_domain_new_domain_mts_crm_password=new_domain
   ```
3. Репозиторий vertis-ansible:
   1. добавить секреты из п.3 для старого деплоя в тестинг и прод (`roles/vertis-datasources-secrets/templates/prod/etc/yandex/vertis-datasources-secrets/telepony.j2`, `roles/vertis-datasources-secrets/templates/test/etc/yandex/vertis-datasources-secrets/telepony.j2`)
   ```
     telepony.domain.new_domain.mts.crm.username = {{lookup('yav', 'sec-01dh1qerwf9mq0ykx48q9wdn1d', 'telepony_domain_new_domain_mts_crm_username')}}
     telepony.domain.new_domain.mts.crm.password = {{lookup('yav', 'sec-01dh1qerwf9mq0ykx48q9wdn1d', 'telepony_domain_new_domain_mts_crm_password')}}
   ```
   2. добавить секреты из п.3 для нового деплоя (не уверен, что это кем-то используется) в тестинг и прод (`roles/vertis-datasources-secrets/templates/prod/etc/yandex/vertis-datasources-secrets/telepony_new_deploy.j2`, `roles/vertis-datasources-secrets/templates/test/etc/yandex/vertis-datasources-secrets/telepony_new_deploy.j2`)
   ```
      SECRET_DOMAIN_NEW_DOMAIN_MTS_CRM_USERNAME = {{lookup('yav', 'sec-01dh1qerwf9mq0ykx48q9wdn1d', 'telepony_domain_new_domain_mts_crm_username')}}
      SECRET_DOMAIN_NEW_DOMAIN_MTS_CRM_PASSWORD = {{lookup('yav', 'sec-01dh1qerwf9mq0ykx48q9wdn1d', 'telepony_domain_new_domain_mts_crm_password')}}
   ```
4. Репозиторий telepony:
   1. Добавляем скрипт `INSERT INTO domain VALUES ($next_id, 'new_domain');` в ../telepony-dao/src/main/resources/sql/shared/${next_id}.sql и ../telepony-dao/src/main/resources/sql/shared/telepony.sql
   2. Добавить новый домен в enum `ru.yandex.vertis.telepony.model.TypedDomains`
   3. Добавляем домен в список `telepony.domains` в конфиге `dao.conf` и `dao.testing.conf`
   4. Добавляем фейковые креды mts.crm в локальные конфиги, шаблоны конфигов и конфиги для teamcity в `secrets.local.template.conf` и `secrets.teamcity.conf` (todo - возможно - это не нужно, т.к. для новых доменов используется shared аккаунт):
   ```
     secrets.telepony.domain.new_domain.mts.crm.username = "fake"
     secrets.telepony.domain.new_domain.mts.crm.password = "fake"
   ```
   5. Добавляем новый домен в доменный конфиг `telepony.domain` в `dao.conf`
   ```
   new_domain {
      operator {
        mts {
          crm {
            url = ${telepony.domain.default.operator.mts.crm.base-url}${telepony.environment}"/new_domain"
            credentials {
              username = ${secrets.telepony.domain.new_domain.mts.crm.username}
              password = ${secrets.telepony.domain.new_domain.mts.crm.password}
            }
          }
        }
        vox {
          //not ready for using
          rule-name = "new_domain_redirect"
        }
      }
    }
   ```
5. После выполнения скриптов базы и мержа в master vertis-ansible выкладываем все компоненты телепони с новым доменом и конфигами
6. (опционально) по базе смотрим, есть ли свободные номера в домене experiments - если есть - наливаем пару номеров в новый домен
и проверяем, что звонок на него проходит и собирается. По согласованию с @bfa можно использовать номера и из других доменов.

На этом домен с дефолтными настройками заведен и готов к работе.

#### Про настройки премедиа
Иногда может потребоваться включить для домена премедиа и какие-то другие недефолтные настройки.
Это потребует дополнительные шаги - настройки мастер номеров для мтс, дополнительные настройки в конфигах и т.п.
На текущий момент в данном гайде эти шаги не описаны.


#### Спорные моменты:
Тут есть существенный кусок про mts.crm, хотя в МТС мы используем shared аккаунт.
На текущий момент без этого домен не заведется. В дальнейшем, нужно выпилить лишний код сперва.
И затем лишние конфиги.
Это очень сильно упростит добавление нового домена.

#### Примеры:
Примеры можно посмотреть в тикетах (там же прилинкованы пулл реквесты гитхаба):
- https://st.yandex-team.ru/TELEPONY-2157
- https://st.yandex-team.ru/TELEPONY-1943
