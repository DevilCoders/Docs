Набор шаблонов для работы с tariff-editor в vs-code.
------

Для написания шаблонов используется плагин [Template Generator](https://marketplace.visualstudio.com/items?itemName=prui.template-generator-vscode), который нужно установить.

**Доступные шаблоны:**

- Функциональный компонент (папка)
- Функциональный компонент (файл)
- Функциональный компонент со стилями (папка)
- Компонент модального окна
- Компонент селекта
- Сага
- Сервис
- Сервис драфтов
- Api

**Для установки шаблонов выполнить:**
```
git clone https://github.yandex-team.ru/dmiadr/tariff-editor-vscode-templates
cd tariff-editor-vscode-templates
npm run install
cd ..
rm -rf tariff-editor-vscode-templates
```
- Команда перетрет только те шаблоны, у которых совпали имена с имеющимися.

Если работаете с использованием Remote Dev, то нужно запускать скрипт на удаленной машинке

После этого в контекстом меню появится пункт создать файл по шаблону:

<img src="https://jing.yandex-team.ru/files/vigdorov/Снимок%20экрана%202020-06-25%20в%2019.55.20.png" width="300" height="186"/>

После выбора шаблона достаточно указать только имя файла, разделяя слова через пробел, тире или используя camelCase. 
Например:
```
discount list
discount-list
DiscountList
```
Создаст файл:
```
DiscountList.tsx
```

Для API, Сервисов, Модалки, Select окончания дописываются автоматом (API, Service, Modal, Select - соответственно).
