## Запуск локального окружения для разработки

Требования: node 12, yarn 1.22.5

### Устанавливаем yarn
Yarn используем версии 1.22.5.
```
npm install --global yarn
```

### Разработка на https://localhost.yandex-team.ru
Авторизация на беке происходит через паспорт. Чтобы подцепилась кука, нужно поднимать локальную разработку на https://localhost.yandex-team.ru.

1) клонируем репозиторий (например в workdir/crm-frontend)   

### Для работы webpack-dev-server и прокси нужены сертификаты
1. Скачиваем файлы из [секретницы](https://yav.yandex-team.ru/secret/sec-01etr65tcyyf91k4shpve0k93f/explore/versions)
2. Добавляем файлы в папку `workdir/crm-frontend/.ssl/`

### Про танкер
Танкер – сервис, хранилище переводов.

Токен нужно положить в переменную окружения TANKER_API_TOKEN или TANKER_TOKEN, либо в корень проекта в файл token (`workdir/crm-frontend/.tanker/token`).
Ссылка для получения токена https://nda.ya.ru/3SjQY7.

### Обновляем host

nano /etc/hosts

```sh
127.0.0.1 localhost.yandex-team.ru
::1 localhost.yandex-team.ru
```

### Устанавливаем зависимости
1) `yarn` – в workdir/crm-frontend

### Запускаем
```sh
sudo yarn serve // sudo нужно чтобы поднимать сервер на 443 порту. Прокси смотрит на тест
sudo yarn serve --env server=dev // прокси смотрит на дев
sudo yarn serve --env serverUrl=https://custom.yandex-team.ru // прокси смотрит на произвольный домен
```

### Войти под другим пользователем
Чтобы зайти под другим пользователем, надо добавить куку devcrm=\<login\>
