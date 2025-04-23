# abc-cli

> CLI-утилита для работы с CLI.

## Установка

```console
npm install @yandex-int/si.ci.abc-cli --registry=https://npm.yandex-team.ru --save
```

## Использование

```console
abc members list infraspeed infratest
abc members list infraspeed infratest --role developer --format "%l"
```

### members

```console
abc.js members <command>

Manages ABC group members.

Commands:
  abc.js members list <services..>  List given ABC group(s) members.
```

#### list

Вывод сотрудников из заданных сервисов.

```console
Positionals:
  services  List of ABC services. Services should be separated with space, and
            can be set after options with --.   [array] [required] [default: []]

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
  --role         Role to filter ABC service members. Multiple options are
                 aggregated as a list of roles.            [array] [default: []]
  --format       Formats output.

                 Available formats:
                 * "%l" - User login.
                 * "%e" - User e-mail.
                 * "%r" - User role.
                 * "%s" - Service name, whom user belongs.
                                                     [string] [default: %l <%e>]

Examples:
  abc members list infraspeed infratest
  abc members list --role=developer
  abc members list --role=developer --role=manager
  abc members list --format="%l" -- infraspeed infratest
  abc members list --role=developer --format="%l %r" -- infraspeed infratest
  abc members list --role=manager --format="%l <%e>, %s" infraspeed
```
