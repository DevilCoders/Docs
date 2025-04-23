<!-- # Линтеры

## Прекоммитные проверки

В директории `/frontend/` настроены прекоммитные проверки для `arc`.

> Подробнее о проверках читайте в [документации](https://a.yandex-team.ru/arc_vcs/frontend/docs/faq/checks.md#линтеры) директории `/frontend/`

### Как отключить лишние проверки?

На данный момент `/frontend/` запрещает добавление новых файлов в директорию `/projects/maps` во время прекоммитных проверок.

> Поведение будет исправлено в рамках [FEI-21213](https://st.yandex-team.ru/FEI-21213).

Чтобы отключить лишние проверки, удалите прекоммит-хук для директории `frontend` в файле `$HOME/.arcconfig`.

```
[pre-commit-hook "frontend"]
    arctic-husky-pre-commit = .arc/user_hooks/hooks/pre-commit
``` -->
TODO