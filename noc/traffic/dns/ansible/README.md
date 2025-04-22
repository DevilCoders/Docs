# Для забывчивых

## Основные команды
```bash
# наш inventory находится в корне этого проекта, файл: hosts

# для тренировки удобно использовать ping
ansible all -m ping --limit 'ns_cache_experiment'

# для раскатки не на все хосты, нужно указывать limit и в нём хосты/группы, можно так же делать иссключения(https://nda.ya.ru/t/dbZV3DzC4rxMp3)
ansible-playbook plays/name-update-unbound-and-unbound64.yaml --limit 'ns_cache_prestable'

# для запуска с кастомными параметрами, нужно найти их в vars(напр. playbooks/roles/unbound-dns64/vars/main.yaml) и запустить с ключом -e
ansible-playbook plays/name-update-unbound-and-unbound64.yaml --limit 'ns_cache_prestable' -e "resource_url=http://s3.mds.yandex.net/... resource_version=1.99.0-r1234567"

```

## Опции которые можно передать с ключом -e
```bash
resource_url=http://s3.mds.yandex.net/....tar.gz # ссылка на бинарь с unbound 
resource_version=1.15.0-r9XXXXXX # версия, которую можно взять из нового сварившегося тарбола с unbound
concurrency_install=1 # на сколько серверов можно параллельно накатывать рецепт
force_install=False   # даже если версия такая установлена всё равно скачать и установить, перезапустить
delete_cache=False    # Если True, то во время установки удаляется yp кеш
ignore_readiness_check=False # игнорировать проверку живости https://localhost:6443/api/v3.0/readiness (некоторые сервера по умолчанию всегда будут проваливать эту проверку)
```
