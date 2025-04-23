## Vertis [dist](https://dist.yandex.net/) pkginfo
====================================
### FIXME:
  Избавиться от side-effect'ов:
  * ~~`pkginfo.utils.logger`~~
  * ~~`pkginfo.__init__`: `umount_ssh_repos`~~
  * Приделать скачивалку всех `Packages.gz` и строить из них локальный индекс (e.g. TTL = 1d)

### Что это такое
  Это небольшой инструментарий для поиска и фильтрации дебиановских пакетов
  на `dist.yandex.ru`. 

#### Например
  Вам нужно найти все пакеты и их владельцев, у которых в зависимостях указана
  необходимая причина поиска таких пакетов. Или все пакеты в тестинге.
  Или все пакеты из кондукторных деплой-листов и тоже как-нибудь их отфильтровать

#### Как это работает
  Не самым технологичным образом, но как-то так:
  * Монтирует `dist.yandex.ru`, `secdist.yandex.ru` по `sshfs`
  * По заданным в сценарии проектным-группам из кондуктора вытаскиваются хосты
  * По этим хостам собирается аггрегированный список пакетов
  * Ищутся deb'ки этих пакетов по порядку в ветках, указанных в `settings.py`
  * Пакет открывается как архив с локального диска (то есть не скачивается),
  * Мапится в память файл `control.tar.gz`, но мы его распаковываем и аггрегируем в словарь
  * По получившемуся списку ищем пакеты, которые подходят под наши критерии
  * Что-нибудь делаем с результатом

#### Как с этим работать
  Вам понадобится установить:
  * `brew install osxfuse sshfs`. Питон 3rd-party:
  * `pip install debian requests colorlog`
  * `git clone git@repo pkginfo`
  Теперь можно править настройки `pkginfo/settings.py` и базовый сценарий
  `pkginfo/scripts/packages-info.py`. Запускать нужно снаружи, например:
  * `python pkginfo/scripts/packages-info.py --depend yandex-memcached-multiple --debug`
  * `python -m pkginfo.scripts.packages-info --depend yandex-memcached-multiple --debug`

#### tree =>
```
pkginfo
├── README.md
├── __init__.py
├── settings.py
├── scripts
│   ├── __init__.py
│   ├── base.py
│   └── packages-info.py
├── tasks
│   ├── __init__.py
│   └── packages.py
└── utils
    ├── __init__.py
    ├── conductor.py
    ├── logger.py
    └── mount.py
```
##### TODO:
  Есть `python-apt` библиотека для работы с libapt, из нее неплохо было бы поюзать apt-cache'вский
  файл `pkgcache.bin`, ведь по нему поиск выполнялся бы в разы быстрее. Можно провести 
  небольшой ресёрч на тему сборки `libapt` под макосом.
  Еще можно самостоятельно построить базу пакетов тупо пройдя в цикле по всем веткам
  во всех репозиториях и выдрать файл `Packages.gz`, но тут возникают проблемы с актуализацией
  базы

  Да и вообще, считаю что до этого `TODO` мы не доберемся, если инструментарий вообще
  понадобится кому-либо :) 

##### НО!
  Если же вам все таки понадобилось что-то отфильтровать на наших репозиториях, то, 
  как видите, пакет разбит на независимые функциональные методы, возвращающие результат. 
  Поэтому построить свой сценарий на основе `scripts/packages-info.py` не составит труда

![](https://leto50d.storage.yandex.net/rdisk/5c1a7d8118e5002675f835e9fd54cdea869d1c5f1b053182cb341c38d492abcd/inf/V_N4yHOZXZwVTl_cRzN0Lsa_2m_8Ku5rkva_ayEFxD5ic039WqCr9kx1bFpznPaqywHbkEExWKcTJvJxJubw6A==?uid=324258310&filename=2015-08-04%2005-16-39%201.%20just%40justbook%3A%20%2Apython%20pkginfo%20scripts%20packages-info.py%20--depend%20yandex-memcached-multiple%20--debug%20%28.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&tknv=v2&rtoken=6dcfb66d52b057e6cd39f1d797b8cdd6&force_default=yes&ycrid=na-60ecc86bd36001301653f58c4df55ccb-downloader8g)
![](https://leto21e.storage.yandex.net/rdisk/0d691c66d0b29dbc36031925cb84f1ba6eb6bb9fae6863b941370cb4731a5b70/inf/Q3b9dg2Uys66kmNtfGJXy5eDvaESX320juu9vhlLbJPqwTJLBnpLyzMb1nW41yCBotVFvOC4t7hzt1kvDS7QcA==?uid=324258310&filename=2015-08-04%2005-23-55%201.%20just%40justbook%3A%20utils%20%28mc%29.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&tknv=v2&rtoken=6dcfb66d52b057e6cd39f1d797b8cdd6&force_default=yes&ycrid=na-5bd2eccac86bcccd36977b01050da451-downloader9g)
