#BuildInventoriServerBinariesDeploy
## Как запустить

```bash
cd ~/arcadia/sandbox/projects/inventori/BuildInventoriServerBinaries/bin

ya make && ./inventori-build-server run --type BUILD_INVENTORI_SERVER_BINARIES --enable-taskbox --create-only
````

После этого может быть наркомания (если все ок и параметры прососались – ниже читать не нужно)

Переходим по ссылке на задачу созданную нашей командой.

Если там нет параметров нужно проставить в **ADVANCED**-> task_id
нужный id-шник который у вас консоли(почему-то туда может подставиться что-то не то).

Нажать save.

После этого все параметры протащаться, нужно выбратать какой серверсайд вы хотите отправить (`media/performance` – radio_button в самом конце списка)
