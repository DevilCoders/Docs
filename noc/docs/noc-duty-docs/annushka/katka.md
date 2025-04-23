# Процедуры обновления annushka
## Наливочная копия annushka

На серверах Racktables есть отдельный инстанс аннушки обновляемый руками который располагается в `/home/racktables/gitworkdir/annushka-production`.

Из него 

* деплоются [project id acl](../racktables/project_id_acl)
* деплоются настройки 802.1X `rt-yandex.git/plugins/8021x.php`
* генерируется выгрузка `getDevMesh` которая используется в `mondata` и `pahom`


### Заводим NOCRFCS

Примеры тикетов

* [NOCRFCS-6158](https://st.yandex-team.ru/NOCRFCS-6158)
* [NOCRFCS-8573](https://st.yandex-team.ru/NOCRFCS-8573)

### Обновляем annushka-production

На всеx серверах Racktables выполняем 
```sh
sudo su -l racktables
cd racktables/gitworkdir/annushka-production
# Бекапим последний рабочий HEAD в локальном бранче
git branch -D last
git checkout -b last
# Стягиваем мастер
git checkout master
git pull
```

> На новые ноды rt деплой происходит автоматически, роботом.  
> Обычно проблемы пользователей возникают из-за устаревшей копии именно на мастере Racktables.

### Обновляем annushka-production/.venv

Если изменились зависимости, либо нужен фикс в например comocutor'e нужно обновить annushka-production/.venv. На всех серверах Racktables выполняем

```sh
sudo su -l racktables
# Бекапим рабочий venv
cd /home/racktables/gitworkdir/annushka-production/
cp -r .venv .venv-`date +'%Y-%m-%d'`
# Устанавливаем последние зависимости ann
.venv/bin/python3 -mpip install -U -r requirements.txt
```
## CK копия annushka
[Процедура описана в разделе ЦК.](../ck/katka.md)
