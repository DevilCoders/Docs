### Настройка tvmtool

[TVM](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/) нужен для хождения между сервисами, в нашем случае в [BlackBox](https://doc.yandex-team.ru/blackbox/tasks/HowToAccessBlackbox.html) для проверки авторизации пользователя.  
Детально ознакомится, что такое TVM и с чем его едят можно [тут](https://github.yandex-team.ru/makishvili/about/blob/master/tvm.md).

#### Установка
Заходим по ssh на сервер и ставим пакет:
```bash
sudo apt-get install yandex-passport-tvmtool
```

#### Настройка
Для начала нужно получить секреты из ABC.  
Переходим [по ссылке](https://abc.yandex-team.ru/services/tvm-callcenter-frontend/resources/), и видим следующий сервис:  
![](abc-resources.png)

кликаем по строке `tvm-callcenter-frontend-testing`, и видим всплывающее окно:  
![](abc-resource.png)
> если не видим, значит нужно запросить роль `TVM-менеджер`.

нам важны следующие поля:
- ID
- name
- client_secret

Теперь когда мы знаем секреты, нам нужно создать файл конфига для tvm-демона. Для этого на сервере выполняем следующую команду:
```bash
sudo vi /etc/tvmtool/tvmtool.conf
```
и копируем в него следующее содержимое:
```
{
  "BbEnvType": 0,
  "clients": {
    "<name>": {
      "secret": "<client_secret>",
      "self_tvm_id": <ID>,
      "dsts": {
        "blackbox": {
          "dst_id": 224
        }
      }
    }
  },
  "port": 8002
}
```
где `<name>`, `<client_secret>` и `<ID>` заменяем на полученные из ABC. Поля `dst_id` и `port` оставляем как есть.  
**Важно! `<ID>` должно быть числом, а не строкой, иначе демон не заведется.**

Сохраняем авторизационный токен в файл:
```bash
sudo vi /var/lib/tvmtool/local.auth
```
и копируем туда строку:
```
tvmtool-development-access-token
```
> Токен менять не нужно, он используется при запуске приложения. Если хочется изменить токен, то не забываем его прописать его в package.json
>
> Вообще токен прописывать не обязтельно, при запуске tvm-демона он создается автоматически по этому пути, но тогда придется самому читать его из файла.

На этом настройку можно считать законченной, осталось запустить демона.

#### Запуск
Ручками:
```bash
sudo service yandex-passport-tvmtool start 
```

Добавить в автозапуск, чтобы демон висел постоянно:
```bash
sudo systemctl enable yandex-passport-tvmtool
```

Статус демона можно узнать командой:
```bash
sudo service yandex-passport-tvmtool status
```

В консоль должно вывестись примерно следующее:  
![](service-yandex-passport-tvmtool-status.png)

Проверить, работает ли демон можно командой:
```bash
curl http://localhost:8002/tvm/ping
```
в консоль должно вывестись **OK**.

TVM-демон готов к работе. **Profit**

#### Не много ссылок
- [лучшее что можно найти про TVM](https://github.yandex-team.ru/makishvili/about/blob/master/tvm.md) читать много, но полезно
- [тестовый ABC сервис](https://abc.yandex-team.ru/services/tvm-callcenter-frontend/resources/?show-resource=5247781)
- [продовый ABC сервис](https://abc.yandex-team.ru/services/tvm-callcenter-frontend-production/resources/?show-resource=5258645)
