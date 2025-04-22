# Тарифы и покупка подписок Яндекс 360

- [Окружения в деплое](https://deploy.yandex-team.ru/projects/ps-tuning)
Катим через `dctl`, так как нужна опция `host_name_kind: persistent`, которая ставит нормальный хостнейм. Это нужно, чтобы можно было далее агрегировать в джаглере
- Графики: [инстансы](https://yasm.yandex-team.ru/template/panel/tuning/), [балансер](https://yasm.yandex-team.ru/template/panel/disk-balancers/-/2/)

### Начало разработки
- [Как поднять окружение в QYP](../../tools/qyp#инструкция)

Перед началом убедитесь, что на машину прокинуты ключи шифрования

```shell script
ssh-add -l
```

К машине по `ssh` надо подключаться с флагом `-A`.

1. Подготовить dev-окружение

```shell script
cd ~/arcadia/yandex360/frontend/services/tuning
npm run prepare-dev
```

2. Запустить проект

```shell script
npm start
```

Для удобства можно в разных вкладках tmux запустить отдельно клиент и сервер
```shell
npm run start:client
npm run start:server
```

3. Для получения ссылки в браузере нужно выполнить `npm run url`. Ссылка в браузере зависит от названия виртуальной машины и датацентра.
Если машина находится в сасово, то адрес будет `https://<vm_name>-arc.tuning-dev.mail.yandex.ru`,
если в другом дц — `https://<dc>-<vm_name>-arc.tuning-dev.mail.yandex.ru`,
где `<dc>` — название датацентра (iva|man|myt|sas|vla),
`<vm_name>` - название виртуальной машины в QYP.
У лендингов адрес имеет вид `https://<vm_name>-arc.360-dev.mail.yandex.ru`


### Переводы

Проект в танкере
`https://tanker.yandex-team.ru/?project=front-ps-tuning&branch=master`

Как скачать переводы

```shell script
npm run tanker
```

### Сборка

Для сборки релиза достаточно выполнить команду

```
npm run package {VERSION} {RELEASE_TICKET}

# например
npm run package 1.0.1 CHEMODAN-123
```

### Сборка слоя 360-landing-override c конфигом Nginx для лендингов
- зайти в папку с образом [disk-front-duffman](https://a.yandex-team.ru/arc_vcs/disk/admin/docker/disk/clusters/disk-front-duffman)
- выполнить команду:
```bash
ya upload -T=DISK_COMPRESSED_RESOURCE_APPLICATION -d='overrides for 360.yandex(|.ru|.com)' --owner DISK-ADMIN --do-not-remove --tar 360-landing/*
```
- на нужном стенде поменять `URL` слоя `360-landing-override` на `sbr:<id>`, где `<id>` - номер собранного ресурса, который вывела команда

### Сборка временного dev-ресурса

**Для прода не подходит!!!**

```
make dev-publish
```

Собирает временный dev-ресурс со встроенной статикой который можно поставить в deploy для тестовых целей.

### Логи

https://wiki.yandex-team.ru/disk/admin/disk-logs-all/#tuning-front

### Лендинги

В тюнинге есть такие лендинги:
- `/jobs` и `/business/education` проксируются в конструктор
- b2c-лендинг раздаётся с `/` с хоста 360.yandex.ru - наш лендинг с React-ом
- `/business`, `/business/tariff`, `/business/tariffeducation` - наши лендинги с React-ом

### Гермиона

_Без указания base-url запускается на проде_

Запустить с выводом в консоль
```
npm run hermione
```

Запустить в интерактивном режиме
```
npm run hermione -- gui
```

Запустить в интерактивном дебаг режиме
```
npm run hermione -- gui --debug
```

Запустить на конкретном урле
```
npm run hermione -- gui --debug --base-url https://tuning.dsp.yandex.ru
```
