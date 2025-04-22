# Как добавить/удалить/изменить статусы

1. Сделать нужные изменения на [тестинге трекера](https://st.test.yandex-team.ru/admin/queue/GOALSVAULTIV/workflows)
2. Добавить статусы в enum статусов: `server/services/goals/interfaces/v2/IGoalStatuses.ts`
3. Если цели в новых статусах должны по умолчанию прорастать в фильтры, то добавить статусы в список дефолтных для старого фронта (`src/js/common/defaultStatuses.js`) и для нового фронта и бека (`server/modules/common/defaultStatusesKeys.ts`)
4. Добавить переводы для новых статусов в 3 файлах в папке `src/i18n`
