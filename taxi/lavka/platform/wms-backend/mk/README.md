# Make recipes

## Bash Strict mode
- По дефолту make-рецепт запускает каждую команду в отдельной subshell
- Если одна из команд в рецепте упадёт, он make продолжит работать дальше
  и вернёт код последней выполненной команды
- Для ожидаемого поведения нужно запускать команды в bash strict mode
- Про bash strict mode
  - http://redsymbol.net/articles/unofficial-bash-strict-mode/

### Strict mode example
Как сказать make'у чтоб запускал рецепт в strict mode

```
.ONESHELL:
SHELL = /bin/bash
.SHELLFLAGS = -ec
IFS = $$'\n\t'
my-recipe:
  $(info Strict mode recipe)
  echo 'bu'
```

