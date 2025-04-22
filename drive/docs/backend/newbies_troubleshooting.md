# Troubleshooting

## `no space left on device`

Закончилось место на диске, в первую очередь пробуем удалить кеш `ya make`:

```(bash)
rm -rf ~/.ya/build
```
## `RSA keys not found`

Не найдены rsa-ключи. Добавляем rsa-ключи на VM. С локального устройства запускаем команду:

```(bash)
scp ~/.ssh/id_rsa vm_hostname:~/.ssh/id_rsa
scp ~/.ssh/id_rsa.pub vm_hostname:~/.ssh/id_rsa.pub
```

Корректируем права доступа к файлам:

```(bash)
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
```

## `No keys in the SSH Agent`

Настраиваем ssh-agent, чтобы в дальнейшем при подключении к удаленному серверу по ключу не вводить заново пароль на ключ.

{% cut "Ubuntu 18.04" %}
Создаём `ssh-agent.service`:

```(bash)
sudo nano /etc/systemd/user/ssh-agent.service
```

В файл записываем:

```
[Unit]
Description=SSH authentication agent

[Service]
ExecStart=/usr/bin/ssh-agent -a %t/ssh-agent.socket -D
Type=simple

[Install]
WantedBy=default.target
```

И запускаем `ssh-agent`:

```(bash)
systemctl --user enable ssh-agent.service
systemctl --user start ssh-agent.service
```

В файл `~/.bashrc` добавляем:

```(bash)
export SSH_AUTH_SOCK="$XDG_RUNTIME_DIR/ssh-agent.socket"
```

Проверяем статус `ssh-agent` и добавляем ключи:

```(bash)
systemctl --user status ssh-agent.service
ssh-add
```
{% endcut %}

Запускаем бекенд:

```(bash)
./drive/devops/cli/cli start-backend
```
