## Как собрать бинарную задачу

### Для linux

    cd sandbox/projects/metrika/mobile/sdk/bin_linux
    ya make --target-platform=DEFAULT-LINUX-X86_64 && ya upload ./bin_linux -T SANDBOX_TASKS_BINARY

---
### Для macOS

    cd sandbox/projects/metrika/mobile/sdk/bin_darwin
    ya make --target-platform=DEFAULT-DARWIN-X86_64 && ya upload ./bin_darwin -T SANDBOX_TASKS_BINARY --arch=osx

---
Подробней про бинарные задачи можно почитать [тут](https://wiki.yandex-team.ru/sandbox/tasks/binary/).
