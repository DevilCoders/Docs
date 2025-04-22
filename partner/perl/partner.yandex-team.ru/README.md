# partner.yandex-team.ru

Source code for site https://partner.yandex-team.ru/

## depoy

ansible-playbook -i hosts ./partner.yandex-team.ru


## build for dev

    time docker build --tag partner-yandex-team-ru .

## run

    time docker run \
        --rm \
        -e "YANDEX_WIKI_OAUTH_TOKEN=$TOKEN_WIKI" \
        -e "STARTREK_OAUTH_TOKEN=$TOKEN_STARTREK" \
        -e "GITHUB_OAUTH_TOKEN=$TOKEN_GIT" \
        --publish 3000:3000 \
        partner-yandex-team-ru

## dev

### run in dev mode

    ./run

### development

<details>
<summary>Команды</summary>

```
# Добавляем Perl модули
vim cpanfile

# Обновляем зависимости
./update_deps


# Собираем образ
sudo docker build --tag devtag .

# Меняем ./run (он только для разработку и по хорошему его вообще нужно удалить)
vim ./run

docker run \
   --rm \
   -it \
   --publish 8409:3000 \                        #  <--- Порт своей беты
   --volume `pwd`/bin/:/app/bin \
   --volume `pwd`/Utils/:/app/Utils \
   -e "YANDEX_WIKI_OAUTH_TOKEN=$TOKEN_WIKI" \
   -e "STARTREK_OAUTH_TOKEN=$TOKEN_STARTREK" \
   -e "GITHUB_OAUTH_TOKEN=$TOKEN_GIT" \
   -e 'SLACK_INTEGRATION_URL=https://hooks.slack.com/services/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' \
   --name "$USER.dev.partner.yandex-team.ru" \  # <--- свой логин
   devtag \                                     # <--- dev таг
   bash -c './cmd'


# Меняем URL, а таже http[S] -> http
#http://partner.yandex-team.ru/api/0/ -> http://<dev-partner2>:<Порт своей беты>
vim bin/app.pl


# Запускаем контейнер (изменения файлов в проекте будут автоматом подтягиваться в контейнере)
./run

# смотрим логи
 docker logs -f  "$USER.dev.partner.yandex-team.ru"

# Если нужно, заходим в контейнер (в другой консоли)
> docker exec -u 0 -it "$USER.dev.partner.yandex-team.ru" bash
> perl  -I./local/lib/perl5  -I./lib  -wc  bin/app.pl
bin/app.pl syntax OK
> cat /data/partner2_pr.json

# В конце, если нужно, ну забываем менять переменные окружения в PARTNER_ANSIBLE
https://github.yandex-team.ru/partner/partner_ansible/blob/master/files/partner.yandex-team.ru/upstart.conf#L10



```
</details>
