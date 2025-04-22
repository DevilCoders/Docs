# Быстрый старт
1. Первое, что нужно сделать - сгенерировать ssh-ключ для авторизации внутри сети:
   – Инструкции для [MacOS](https://wiki.yandex-team.ru/diy/macos/ssh/), [Windows (+ PuTTY)](https://wiki.yandex-team.ru/diy/windows/ssh/) и [Linux](https://wiki.yandex-team.ru/diy/linux/ssh/)
2. Публичный ключ нужно скопировать текстом и загрузить на https://staff.yandex-team.ru:
     ![public key](./images/quick-start-pubkey.png)
  После этого ключ сам скопируется на те машины, на которые ты можешь ходить по SSH. Это занимает некоторое время, но в течение дня он должен разъехаться.

## Установка Arc
Если [Arc](https://wiki.yandex-team.ru/verticals/frontend/arc-how-to/#chtotakoearc/arcadia/arcanumikaksjetimzhit) еще не установлен, то воспользуйся [инструкцией по установке](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

При монтировании лучше всего использовать флаг `--allow-other`, это позволит запускать внутри Аркадии команды из под рута.
1. в `/etc/fuse.conf` раскомментить строчку `user_allow_other`
2. Смонтировать с флагом `--allow-other`
```
arc mount ~/arcadia --allow-other
```

Больше информации про Arc, Аркадию и Arcanum смотри в [how-to](https://wiki.yandex-team.ru/verticals/frontend/arc-how-to/)

## Настройка окружения
// todo

## Разворачивание рабочей копии
> **Убедись, что у тебя установлен и используется npm ^7**

```
git clone git@github.com:YandexClassifieds/internal-frontend.git
cd internal-frontend
npx secrets-to-dotenv # загружаем секреты
npm ci # устанавливаем зависимости
npm run install-ssl-cert # скачиваем ssl-сертификат
npm run update-hosts # добавляем локальный домен в /etc/hosts (потребует ввода пароля). Если ругается, попробуй отмонтировать arc и примонтировать заново с флагом --allow-other
cd <PROJECT_NAME> # переходим в директорию проекта, editor-www например
npm run dev # запускает проект в режиме разработки
```

Локальная сборка будет доступна по адресу: https://local.vertis.yandex-team.ru/
