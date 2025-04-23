# <%= projectName %>

Шабллон проекта на [Next.js](https://nextjs.org/)

## Начало работы с шаблоном

```bash
# Копируем шаблон
cp -R frontend/packages/next-template frontend/services/<%= projectName %>
```

Поле этого необходимо заменить все вхождения `<%= projectName %>` в проекте на имя вашего сервиса

## Устанновка

[Как установить brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/)

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12 версии
nvm install 12

# Устанавливаем зависимости монорепозитория
cd frontend
npm i

# Устанавливаем зависимости сервиса
cd services/<%= projectName %>
nvm use
npm run deps

# Задаём переменную окружения для локальной разработки
export NODE_ENV=local
```

Сохраняем в корень проекта файл `.tvm.json`.

```json
{
  "BbEnvType": 1,
  "clients": {
    "<%= projectName %>": {
      "secret": "XXXX",
      "self_tvm_id": 1111,
      "dsts": {
        "blackbox": {
          "dst_id": 224
        }
      }
    }
  }
}
```

## Разработка

```bash
# Локальный запуск
npm run dev
```

Сервис становится доступен по адресу: http://127.0.0.1

### HTTPS

Документация по запуску сервиса на https находится [здесь](https://wiki.yandex-team.ru/bliss/next-template/docs/#zapuskservisanahttps)

### Плагины VSC

- [EditorConfig](https://marketplace.visualstudio.com/items?itemName=editorconfig.editorconfig)
- [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
- [StyleLint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
- [PostCSS Language Support](https://marketplace.visualstudio.com/items?itemName=csstools.postcss)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## Синхронизация переводов

Для загрузки и обновления переводов используется пакет [`tanker-kit`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tanker-kit). Для его работы требуется установить в переменную OAuth-токен: https://nda.ya.ru/3SjQY7

```bash
export TANKER_OAUTH_TOKEN=xxxx;

npm run tanker:pull # Выгрузить переводы
npm run tanker:push # Загрузить переводы
```

## Документация

Актуальная информация по проекту [находится на wiki](https://wiki.yandex-team.ru/next-template/docs/)
