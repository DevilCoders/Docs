# Parks-Front

[![](https://garage.yandex/driver-front/drivers_images/yandex_logo_beta.svg)](https://garage.yandex/taxiparks)

Личный кабинет таксопарка

## Хосты
### dev

http://ytmp-stage2.inno.co/taxiparks

### test

https://marketplace-backend.taxi.tst.yandex.net/taxiparks

[qloud-testing](https://platform.yandex-team.ru/projects/taxi-outsource-marketplace/backend/testing)

### prod

https://garage.yandex/taxiparks

[qloud-stable](https://platform.yandex-team.ru/projects/taxi-outsource-marketplace/backend/stable)

## Как зайти в Личный кабинет

### dev
Заходим сюда http://ytmp-stage2.inno.co/taxipark/account
Вводим название парка и любой ID, если парк есть он зайдет в него, если нет создаст новый.

### test, stable
Идем в ЛК https://marketplace-backend.taxi.tst.yandex.net/taxiparks (test)
https://garage.yandex/taxiparks (stable)

1) Нажмаем "Войти", перекинет в Таксометр
2) Выбираем "Войти через паспорт", выбираем email зарегистрированный в Гараже, выбираем парк
3) После входа, перекинет в админку Таксопарка, там выбираем в меню "Автопарк" -> "Сдать авто в аренду"

## Подготовка
Для работы потребуется Node.js 14.

Для локальной разработки мы используем [NVM](https://github.com/nvm-sh/nvm).

Устанавливаем NVM, а затем:
```bash
# Устанавливаем Node.js 14 версии
nvm install 14

# Переключаемся на эту версию
nvm use 14
```

## Настройка проекта

```bash
# установить зависимости
npm ci
```

## Запуск

```bash
npm start
```

Смотреть после запуска тут: [http://localhost:3000/](http://localhost:3000/).

## Deploy
Делаем по аналогии с [инструкцией для garage-drivers-front](https://a.yandex-team.ru/arc_vcs/taxi/garage-drivers-front#deploy). Если шаги по получению доступа до образа, авторизации в облаке проекта и добаления учетных записей кластеров Kubernetes уже были проделаны (они общие для всех репозиториев Гаража), то их следует пропустить.
