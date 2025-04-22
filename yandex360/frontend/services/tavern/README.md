
# Таверна
Дом общих виджетов Яндекс.360. 

## TL;DR
Сервис, предоставляющий общие виджеты для сервисов 360. Имеет свой фронтбек для наливки данных в виджеты. Встраивается в различные сервисы через iframe (web) или webview (мобильные приложения).
| ![iframe](https://jing.yandex-team.ru/files/temasus/Untitled%203-1.jpg)      | ![шторка](https://jing.yandex-team.ru/files/temasus/Untitled%203-2.jpg) |
| ----------- | ----------- |

 * Чат https://t.me/+KNHrW2vzvKdhZDgy
 * Команда: https://abc.yandex-team.ru/services/tavern
 * Wiki: soon
 * Трекер: https://st.yandex-team.ru/PSTAVERN
 * Проект в деплое https://deploy.yandex-team.ru/projects/tavern
 * NS в awacs L3+L7 (prod) https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tavern.production.mail.yandex.net/show
 * Прод: https://tavern.mail.yandex.ru
 * Общий Dev-стэнд: https://tavern-prestable.mail.yandex.ru

**Мониторинг**

 * Общий дашборд https://yasm.yandex-team.ru/panel/temasus.tavern-main 
 * Логи AWACS балансера *soon*
 * Логи приложения в YT https://yt.yandex-team.ru/hahn/navigation?filter=tavern&path=//home/logfeller/logs 
 * Логи (стрим) https://wiki.yandex-team.ru/pochta/sre/mail-logs/#tavern
 * Ошибки фронта (iframe) https://error.yandex-team.ru/projects/tavern/projectDashboard?filter=platform%20%3D%3D%20desktop
 * Ошибки фронта (шторка) https://error.yandex-team.ru/projects/tavern/projectDashboard?filter=platform%20%3D%3D%20turbo-app
 * Дашборд фронта (iframe) https://rum.yandex-team.ru/projects/tavern?filter=platform%20%3D%3D%20desktop
 * Дашборд фронта (шторка) https://rum.yandex-team.ru/projects/tavern?filter=platform%20%3D%3D%20turbo-app
 * Алерты https://juggler.yandex-team.ru/project/tavern360/dashboard?project=tavern360


**Документация**
В директории [docs](./docs) есть немного документации: по инфре, для интаграции в собильные приложения ("шторка"), 


---------------------------------

Таверна состоит из:
 - клиентских приложений: **iframe** сборкаи и webview сборки (ака **шторка**)
 - **фронтбека**, в основном решает задачу получаения данных для виджетов
 - **портала** (react компонента для встраивания таверны в другие сервисы)
 - **демо стенда** для тестирования портала

## Разработка
 - получить роль "Разработчик интерфейсов" в [ABC](https://abc.yandex-team.ru/services/tavern)
 - завести себе разработческую машину в QYP с пресетом Mailfront по [инструкции](https://github.yandex-team.ru/personal-services/frontend/tree/dev/tools/qyp)
 
### Первоночальная настройка
Ставим зависимости:
```bash
npm ci
```
Получаем секреты:
```bash
make secrets
```

Теперь нужно настроить машинку.

Если у вас **QYP** машина делаем:
```bash
cd ../../tools/qyp
make Mailfront
```

### Как запустить
Если хочется разрабатывать фронтбэк таверны и/или демостенд, то:
```bash
npm start
```

Это запустит дев сборку клиента, фронтбека и демостенда:
 - aдрес самой таверны – `https://XXX.tavern-dev.mail.yandex.ru/`
 - aдрес демостенда – `https://XXX.taverndemo-dev.mail.yandex.ru/`
Где `XXX` имя вашей qyp машины.

Сборка шторки и айфрема более детально описана в [./client](./client).

---

Если хочется разрабатывать еще и портал, то линкуем его локально и запускаем инкрементальную сборку:

```bash
npm --prefix demo run link-tavern-portal
npm --prefix portal start
```
Плюс захардкодить `https://XXX.taverndemo-dev.mail.yandex.ru/` в `demo/features/app/components/App/App.tsx`
