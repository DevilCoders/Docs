# Linux DPDK

Тут у нас хранится сборка поискового ядра с конфигом, слегка затюненным под DPDK нужды.

#### Я хочу новую версию ядра
- Идем в наш форк https://bb.yandex-team.ru/projects/NOC/repos/linux/browse
- Фетчим из апстрима нужную версию, чекаутимся на нее:
  ```
  git checkout release/v5.4.110-13
  ```
- Правим конфиг ядра в `debian/configs/config`.
- Создаем новую ветку или тег. Пусть будет ветка:
  ```
  git checkout -b release/v5.4.110-13+dpdk
  ```
- Бампаем ченджлог и коммитим:
  ```
  VERSION=$(dpkg-parsechangelog -Sversion)+dpdk
  DEBFULLNAME="Evgeny Safronov" DEBEMAIL=esafronov@yandex-team.ru dch --newversion=${VERSION} --distribution=unstable --urgency=low 'modified kernel for DPDK'
  git add debian/configs/config debian/changelog
  git commit -m "release: v${VERSION}"
  git push -u origin release/v5.4.110-13+dpdk  
  ```
- Правим новую версию в `a.yaml`.
- Запускаем сборку.

#### Я хочу собрать ядерные модули DPDK для новой версии ядра
- Собираем ядро (см. выше).
- Собираем в докере dpdk-kernel-modules, получая архив с необходимыми модулями:
  - `docker build . --build-arg=LINUX_KERNEL_VERSION=5.4.110-13+dpdk --progress=plain -t dpdk-kernel-modules`
  - `docker run --rm --entrypoint cat dpdk-kernel-modules /build.tar.gz > build.tar.gz`
- Заливаем в сандбокс, получаем номер ресурса: `ya upload build.tar.gz --do-not-remove`.
- Проставляем номер ресурса в `dpdk-kernel-modules/ya.make`.
- Дергаем `ya make`, либо запускаем через CI.
