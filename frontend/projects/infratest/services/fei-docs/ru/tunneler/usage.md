# Как использовать Tunneler в своём проекте

## Из shell

При помощи пакета [devkit](https://a.yandex-team.ru/arc_vcs/frontend/packages/devkit).
Поставить nodejs, обычно для этого используется [node version manager](https://github.com/nvm-sh/nvm). Можно использовать nodejs из ОС, но там обычно версии совсем старые, нам нужна 10+.
Если нужно запустить разок и не оставлять следов в ОС:
```
npm_config_registry=http://npm.yandex-team.ru/ npx -p @yandex-int/devkit dk tun 3000:2000-50000
```
Скачает код пакета, запустит, потом всё почистит.

Если хочется поставить один раз, чтобы не качать, то можно поставить пакет глобально:
```
npm install -g @yandex-int/devkit
dk tun 3000:2000-50000
```

## Из произвольного js-кода

С помощью [@yandex-int/tunneler](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/tunneler).

## Из проекта, использующего archon

С помощью [@yandex-int/archon-tunneler](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_moduli_s_komponentami_i_komandami/archon-tunneler.html).

## Из проекта, использующего hermione-тесты, но не archon

С помощью [@yandex-int/tunneler](https://doc.yandex-team.ru/si-infra/hermione/hermione_plaginy/tunneler.html) для других проектов.

## Если возникли трудности

Если вы ещё не использовали Tunneler в своём сервисе, и хотите начать, напишите нам на [INFRADUTY](https://wiki.yandex-team.ru/infraduty/form/). Ответьте на такие вопросы:

- Какой ваш сервис в ABC?
- Для чего хотите использовать Tunneler?
- Если для hermione-тестов, расскажите о предполагаемой нагрузке: сколько у вас тестов, как часто они запускаются и т.п.
- Если хотите использовать Tunneler в вашем CI, укажите, какой CI вы используете.

Мы выдадим необходимые доступы и подскажем, как корректно подключить наши модули.
