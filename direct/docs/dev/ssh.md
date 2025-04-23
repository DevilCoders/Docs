# Настройка ssh

{% note info "Более подробные общеяндексовые инструкции" %}

- [https://wiki.yandex-team.ru/security/ssh/macos/](https://wiki.yandex-team.ru/security/ssh/macos/)
- [https://wiki.yandex-team.ru/security/ssh/linux/](https://wiki.yandex-team.ru/security/ssh/linux/)
- [https://wiki.yandex-team.ru/security/ssh/#instrukciiponastrojjkessh-klientov](https://wiki.yandex-team.ru/security/ssh/#instrukciiponastrojjkessh-klientov)

{% endnote %}

## Сгенерировать ssh-ключи

- Создать директорию `~/.ssh`, если её нет `mkdir ~/.ssh`
- Перейти в неё `cd ~/.ssh`
- Сгенерировать ключ `ssh-keygen -t rsa -b 2048 -C staff-login@yandex-team.ru`

```
$ WORK_EMAIL=staff-login@yandex-team.ru
$ ssh-keygen -t rsa -b 2048 -C $WORK_EMAIL
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<staff-login>/.ssh/id_rsa): <ENTER>
Enter passphrase (empty for no passphrase): <ENTER>
Enter same passphrase again: <ENTER>
Your identification has been saved in /home/<staff-login>/.ssh/id_rsa.
Your public key has been saved in /home/<staff-login>/.ssh/id_rsa.pub.
...
```

## Положить публичный ключ на staff

- Выполнить `cat ~/.ssh/id_rsa.pub` в консоли, скопировать содержимое в буфер обмена
- Перейти на [staff](https://staff.yandex-team.ru)
- Найти внизу раздел SSH-ключи, нажать на "карандаш" для редактирования
- Нажать "Добавить ключ"
- В "Ключ" вставить содержимое `id_rsa.pub`
- В "Описание" напишите любое описание компьютера на котором лежит ключ (или всё что угодно)
- Нажать "Сохранить"

После сохранения ключа в пределах получаса ваш ключ раскатится на машинки
с [CAuth](https://wiki.yandex-team.ru/intranet/cauth/), к которым у вас есть доступ.

## Настройка ssh-agent

{% list tabs %}

- MacOS, Linux

  Дописываем в `~/.ssh/config`
  ```
  Host *
    UseKeychain yes
    AddKeysToAgent yes
    IdentityFile ~/.ssh/id_rsa
    
  Host ppcdev*
    ForwardAgent yes
  ```

{% endlist %}
