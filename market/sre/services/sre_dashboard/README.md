## **Backend**

### **Dev Build**
Сборка осуществляется с помощью ya make:
```shell
ya make --add-result=py --add-result=pyi
```
### **Dev Run**
Для запуска надо выпустить [токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=52dbbc853b65412d873d098bc4e81785) и положить его в `~/.sredash/token`
Запустить командой:
```shell
./sre-dashboard --config dev-config.yaml
```
Дешборд должен подняться по url http://localhost:8069
### **Tests**
Для прогона всех тестов включая тесты на типизацию надо выполнить:
```shell
ya make -tt
```

## **Frontend**

### **Prepare**
Работать надо из папки фронтенда:
```shell
cd frontend
```
node_modules лучше хранить вне аркадии, поэтому рекомендую создать симлинк:
```shell
ln -s ~/repos/sre-dash-frontend/node_modules node_modules
```
Это сильно ускорит работу с ними.
Далее выкачиваем нужные зависимости:
```shell
npm ci --registry=https://npm.yandex-team.ru --force
```
Регестри вообще лучше прописать в конфиге:
```shell
echo "registry=https://npm.yandex-team.ru/" >> ~/.npmrc
```
### **Dev Run**
Запускаем командой:
```shell
npm run start
```
Фронтенд ожидает что на http://localhost:8069 запущен бекэнд
### **Tests**
Пока только в ручную `npm run test`
### **Nodemodules deploy**
Чтобы задеплоить новые node_modules в сендбокс, надо:
1. Происнсталить актуальный набор node_modules:
    ```shell
    npm ci --registry=https://npm.yandex-team.ru --force
    ```
2. Перейти в папку в которой храняться node_modules
    ```shell
    cd $(readlink node_modules)/..
    ```
3. Запоковать node_modules в архив:
    ```shell
    tar -czf node_modules.tar.gz node_modules
    ```
4. Залить архив в sandbox:
    ```shell
    ya upload --ttl=inf -d="market-sre sre-dashboard node_modules" --owner=MARKETSRE --sandbox-mds node_modules.tar.gz -T MARKET_SRE_DASHBOARD_NODEMODULES
    ```
5. Поменять id ресурса в `ya.make` и удалить атрибут inf старому ресурсу в сендбокс, чтобы он больше не занимал квоту

## **Node update**
Нода обновляется вручную, путем скачивания ее из офф репозитория и заливкой в сендбокс:
```shell
ya upload --ttl=inf -a=linux -d="node for market-sre tools" --owner=MARKETSRE --sandbox-mds node.tar.gz -T MARKET_SRE_NODEJS
```
Важно чтобы архив назывался node.tar.gz (и был пожат gzip, а не xz как в дефолтной linux поставке nodejs)
