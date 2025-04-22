# Настройка окружения

Здесь собрана полезная информация по настройке клиентов почты/календаря/консоли, а так же о том как создать ssh ключи.

## Почта

Почта это способ гарантированно донести важную информацию до сотрудника. Удобней всего пользоваться Mail.app, которая уже предустановленна на MacBook. Так же у почты есть web интерфейс, доступный по [https://mail.yandex-team.ru](https://mail.yandex-team.ru).

Инструкция по настройке клиента доступна [здесь](https://mail.yandex-team.ru).

{% note tip %}

Настраивать фильтры рекомендую в web ui. 

{% endnote %}

Список рассылок, на которые необходимо подписаться (способ подписки "общая папка"):
- [verstka](https://ml.yandex-team.ru/lists/verstka/)
- [super-dev](https://ml.yandex-team.ru/lists/super-dev/)
- [taxi-dev](https://ml.yandex-team.ru/lists/taxi-dev/)
- [digest-frontend](https://ml.yandex-team.ru/lists/digest-frontend/)
- [go-releases](https://ml.yandex-team.ru/lists/go-releases/)
- [zapusk](https://ml.yandex-team.ru/lists/zapusk/)

## Календарь

Все встречи создаются через [календарь](https://calendar.yandex-team.ru). Для просмотра встреч, удобно пользоваться iCalendar, предустановленный на Mac он удобен тем, что позволяется включить напоминания о встрече за 5 минут до начала.

Инструкция по настройке [здесь](https://doc.yandex-team.ru/calendar/common/sync/sync-desktop.html#customize-sync)

## Staff

staff содержит информцию о сотрудниках компании. Ваша карточка доступа по адресу [https://staff.yandex-team.ru](https://staff.yandex-team.ru).

Необходимо привязать к стафу:
1. ваш внешний яндекс логин (тот, что на yandex.ru), 
2. номер телефона (многие процессы завязаны на телефон, например наличие экспериментов или дежурства)
3. телеграмм аккаунт (без этого автоматика будет выкидывать вас из рабочих чатов)

## Настройка рабочей среды

{% note tip %}

Программа Self Service (установлена на ваш mac) содержит библиотеку приложений, которые разрешены к использованию. От туда можно взять WebStorm, VS Code, Tunnelblick (VPN). Так же сервис позволяет настроить принтеры.

{% endnote %}

### HomeBrew
Установка утилит осуществляется через [Homebrew](https://brew.sh/), поэтому убедитесь, что он установлен и обновлен:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew update
```

### Устанавливаем iTerm2
Для доступа к консоле мы используем **iTerm2**. Поставить его можно через Self Service. 

### Устанавливаем (Обновляем) xcode

Сделать можно через App Store (создать новый аккаунт или войти под вашим личным).

### Генерируем ssh ключ 
__(необходим для доступов на удалённые машинки и других процессов)__

Открываем iTerm2 или стандартную консоль

{% cut "1. Сгенерируйте пару ключей" %}
```bash
mkdir -p ~/.ssh
cd ~/.ssh

# В качестве your-login указываем ваш логин на staff
# После ввода: имя файла оставляем по-умолчанию
# Опция -m PEM фиксит нестандартное поведение в Mojave,
# подробнее: https://serverfault.com/questions/939909/ssh-keygen-does-not-create-rsa-private-key
ssh-keygen -m PEM -t rsa -b 2048 -C your-login@yandex-team.ru

# Устанавливаем нужные права на директорию и файлы
chmod 700 ~/.ssh
chmod 644 ~/.ssh/id_rsa.pub
chmod 600 ~/.ssh/id_rsa

# Добавляем ssh ключ в ssh Agent
ssh-add ~/.ssh/id_rsa
```
{% endcut %}

{% cut "2. Авторизуйся на Staff и добавь ключ" %}

1. `pbcopy < ~/.ssh/id_rsa.pub`
2. Идём на [staff](https://staff.yandex-team.ru) и нажимаем на карандашик возле SSH-ключи, вставляем из буфера ключ

![screen](https://jing.yandex-team.ru/files/twin/Снимок%20экрана%202017-03-20%20в%2019.35.28.png)

{% endcut %}

### Установка arc

Большинство исходников кода храниться внутри монорепозетория яндекса - аркадия.
Необходимо ознакомиться с [документацией](https://docs.yandex-team.ru/arc/) и установить arc.

Большинство проектов фронтенда такси живут в директории [/taxi/frontend](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/frontend/) 