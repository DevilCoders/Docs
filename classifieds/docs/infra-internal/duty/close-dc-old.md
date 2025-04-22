# Старый способ закрытия датацентра

При закрытии рекомендуется использовать drills-helper  там, где это возможно.

Пока мы не умеем полноценно работать без одного дц, делаем следующее:

1. [Смотрим](https://grafana.vertis.yandex-team.ru/d/I1-gRG8Zk/drills-overview?orgId=1&refresh=1m) где находятся мастера Teamcity/Jenkins/Rundeck (строка Admin services status )

2. Изменить мастер-инстанс для:
    * Teamcity

        `drills-helper switch teamcity --from <dc>`
    * Jenkins
        `drills-helper switch jenkins --from <dc>`
    * [Rundeck](https://wiki.yandex-team.ru/vertis-admin/rundeck/#drills)

    **Ручной способ, если что-то пошло не так:**

    * [Jenkins](../services/ci/jenkins.md#pereklyuchenie-v-drugoj-dc)

    * [TeamCity](../services/ci/teamcity.md#pereklyuchenie-v-drugoj-dc)
3. Выключаем деплой

   `drills-helper deploy disable all -d <dc> -l prod `

   **Ручной способ, если что-то пошло не так**

   Выключаем деплой в прод у Jenkins (https://wiki.yandex-team.ru/vertis-admin/docker-deploy/faq/#kakotkljuchitdeplojjvprod).

   Выключаем деплой в shiva (OAUTH_TOKEN  можно взять по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1f82008746cd4bcfb3e2679e747974f9))

   Выключаем деплой в прод в Кондукторе, снимая галочки с prestable и stable на странице https://c.yandex-team.ru/projects/vertis/deploy_schedule, не забываем сохранить изменения.

4. Закрыть от нагрузки load balancers (открытие кластеров выполняется в обратной последовательности):

   Cнимаем новый трафик: `drills-helper lb close ingress -d <dc> `

   Ждем 5 мин, смотрим на графики;

   Закрываем upstream-ы: `drills-helper lb close upstream -d <dc> `

   Закрываем envoy: `drills-helper lb close lb-int -d <dc> `

   Закрываем внутренние lb с nginx: `drills-helper lb close lb-int-nginx -d <dc> `

   **Ручной способ, если что-то пошло не так**

   `%vertis_prod_lb`:
   Через iptruler снимаем новый трафик (пример для sas: `p_exec %vertis_prod_lb@<dc> iptruler all down`);

   Ждем 5 мин, смотрим на графики;

   Через upstream_mngr закрываем бекенды (пример для sas: `p_exec %vertis_prod_lb upstream_mngr -cd <dc> -y`);

   `%vertis_prod_lb_int`:

   `p_exec %vertis_vprod_lb_int@<dc> curl -X POST http://localhost:8001/healthcheck/fail && sleep 15 ; iptruler 1700 down haproxy; sleep 15; iptruler 80 down syn`

   `p_exec %vertis_prod_lb_int@<dc> curl -X POST http://localhost:8001/healthcheck/fail && sleep 15 ; iptruler 1700 down haproxy; sleep 15; iptruler 80 down syn`

   `p_exec %vertis_vprod_lb_int@<dc> curl -X POST http://localhost:8001/healthcheck/ok && sleep 15 ; iptruler 1700 up haproxy; sleep 10 ; iptruler 80 up syn`

   `p_exec %vertis_prod_lb_int@<dc> curl -X POST http://localhost:8001/healthcheck/ok && sleep 15 ; iptruler 1700 up haproxy; sleep 10 ; iptruler 80 up syn`

   `%vertis_vprod_lb_int_nginx`:
   через iptruler (`exec %vertis_vprod_lb_int_nginx@<dc> iptruler all down; iptruler 80 down syn`)

5. Проставляем downtime для ДЦ на корневую кондукторную группу vertis.

   `drills-helper dt 2h -l prod -d <dc> `

   **Старые способы**

   Можно делать в [web-интефейсе juggler](https://juggler.yandex-team.ru/downtimes/). Пример selector-а для SAS: `host=CGROUP%vertis@dc=sas & namespace=vertis`.

   Можно использовать скрипт. Пример вызова скрипта для SAS: `./setDTperDC -dc=sas`;

6. Закрываем ДЦ через HBF, как описано тут https://docs.yandex-team.ru/classifieds-ops-internal/duty/hbf-close-open.

   **Ручной способ, если что-то пошло не так**

   Чтобы закрыть HBF _наверняка_, нужно так же вручную прогнать роль:
   ```
   ansible-playbook hbf_close.yml -e "host=vertis_vprod_docker dc=vla"
   ansible-playbook hbf_close.yml -e "host=vertis_vprod_consul_server dc=vla"
   ```
   Соответственно для открытия нужно сделать:
   ```
   ansible-playbook hbf_open.yml -e "host=vertis_vprod_consul_server dc=vla"
   ansible-playbook hbf_open.yml -e "host=vertis_vprod_docker dc=vla"
   ```
   Вариант через ansible на примере MYT:
   ```
   ansible -mshell -a 'iptruler all down' vertis_prod_lb -l '*myt*' --become
   ansible -mshell -a 'upstream_mngr -cd myt -y' vertis_prod_lb --become

   ansible -mshell -a 'iptruler 1700 down syn; sleep 15; iptruler 80 down syn' vertis_prod_lb_int  -l '*myt*' --become
   ansible -mshell -a 'iptruler all down' vertis_vprod_lb_int_nginx -l '*myt*' --become
   ansible -mshell -a 'iptruler 80 down syn' vertis_vprod_lb_int_nginx -l '*myt*' --become

   grpcurl -d '{"list":[{"name":"ProdMytOff", "reason":"Учения"}, {"name":"ProdSasOff", "reason":"Учения"}, {"name":"ProdYdSasOff", "reason":"Учения"}, {"name":"ProdYdVlaOff", "reason":"Учения"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.SetFlags
   ```
