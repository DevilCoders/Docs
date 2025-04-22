# Порядок работы с пакетами

Для создания, сборки и выкладки пакета необходимо выполнить следующие действия:

1. Убедиться, что на персональном компьютере или сервере, использующемся для сборки пакета, установлено [необходимое программное обеспечение](../Software.md).
    
1. [Сгенерировать GPG-ключи](../GPG.md), которые будут использоваться для подписывания пакетов (минимальная длина — 2048 бит).

    1. Выполнить:
       ```no-highlight
       gpg --gen-key
       ```

    1. Добавить в `~/.bashrc` строки вида:

       - Для версий `dch` младше 2.11.8:
          ```no-highlight
          export DEBFULLNAME="Ivan Ivanov"
          export DEBEMAIL="mylogin@yandex-team.ru"
          alias dch='dch --distributor=debian'
          ```
   
       - Для версий `dch` 2.11.8 и старше:
          ```no-highlight
          export DEBFULLNAME="Ivan Ivanov"
          export DEBEMAIL="mylogin@yandex-team.ru"
          alias dch='dch --vendor=debian'
          ```

1. [Получить доступ к загрузке в репозиторий](../Repos.md) пакетов, подписанных сгенерированными GPG-ключами:
    
    1. Экспортировать публичный GPG-ключ:

       ```no-highlight
       $ gpg --export --armor mylogin@yandex-team.ru >mylogin.gpg
       ```

    1. Добавить содержимое полученного файла на Стафф.
    1. Создать или изменить `~/.dupload.conf`:
    
       ```no-highlight
       
       package config;
       ...
       $default_host = "common";
       $cfg{'common'} = {
       fqdn => "common.dupload.dist.yandex.ru",
       method => "scpb",
       incoming => "/repo/common/mini-dinstall/incoming/",
       dinstall_runs => 0,
       };
       ...
       $cfg{"dist"}{"login"} = "mylogin";
       1;
       
       ```
       
       {% note info %}
       
       На части разработческих машин используется глобальный `dupload.conf`. Создание и/или изменение `~/.dupload.conf` не требуется.
       
       {% endnote %}
       
1. [Создать пакет](../Building.md):
    
    1. Выполнить:
       
       ```no-highlight
       cd
       mkdir -p packages/mypackage-1.0
       cd packages/mypackage-1.0
       $ dh_make -c gpl -n
       ```
       
       {% include [Building-buildingnote](../_includes/concepts/Building/id-Building/buildingnote.md) %}
       
    1. [Внести изменения](../Building.md#ModifyingTemplates) в файлы `control` и `rules`.
    
1. Собрать и подписать пакет:
    
    ```no-highlight
    debuild
    ```
    
    {% include [Building-debuild_results](../_includes/concepts/Building/id-Building/debuild_results.md) %}
    
    {% include [Structure-tip-dpkg-c](../_includes/concepts/Structure/id-Structure/tip-dpkg-c.md) %}
    
1. [Загрузить пакет в репозиторий](../Uploading.md):
    
    ```no-highlight
    debrelease
    ```
