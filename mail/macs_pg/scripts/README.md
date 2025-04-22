
## generate_enums

Генерирует `macs_pg::Enumeration` из `enum` в Postgre (по умолчанию ходим
в локальную базу `--dsn=postgres://localhost/maildb)`)

    python scripts/generate_enums.py mail.change_type ChangeType \
        > include/internal/changelog/change_type.h
