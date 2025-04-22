# yappy-garbage-collector

Временный костыль для [FEI-16587](https://st.yandex-team.ru/FEI-16587).

Удаляет протухшие yappy-беты. Бета считается протухшей, если соответствующий ей пулреквест закрыт. Номер пулреквеста вычисляется по суффиксу `pull-(\d+)`.

Usage:

```
npx @yandex-int/yappy-garbage-collector --quota report-renderer-templates --owner search-interfaces --repo frontend
```

Шедулер для frontend: https://sandbox.yandex-team.ru/scheduler/705859/view
